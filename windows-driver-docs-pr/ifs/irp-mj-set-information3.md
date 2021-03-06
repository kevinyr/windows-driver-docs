---
title: IRP\_MJ\_SET\_INFORMATION
author: windows-driver-content
description: IRP\_MJ\_SET\_INFORMATION
ms.assetid: 2a6c837c-85c9-46d8-85d8-d779f22be54e
keywords: ["IRP_MJ_SET_INFORMATION", "security WDK file systems , adding security checks", "security checks WDK file systems , IRP_MJ_SET_INFORMATION", "rename operations WDK file systems", "hard link operations WDK file systems", "names WDK file systems"]
---

# IRP\_MJ\_SET\_INFORMATION


The rename and hard link cases in set information might require a security check under certain circumstances. Specifically, if the caller wants to delete the target of the rename or hard link by setting the **ReplaceIfExists** field to **TRUE**, the file system must perform a security check to ensure that the caller has appropriate permission to delete the target. In addition, there can be certain types of files that the file system, as a matter of policy, does not wish to allow to be deleted in this fashion (registry hives and paging files, for example). The following code example determines if the caller has the appropriate security permissions to delete the file:

```
NTSTATUS FsdCheckDeleteFileAccess(POW_IRP_CONTEXT IrpContext, 
                                  PSECURITY_DESCRIPTOR targetSD, 
                                  PFCB ParentFcb)
{
    SECURITY_SUBJECT_CONTEXT SubjectContext;
    BOOLEAN Granted;
    NTSTATUS status = STATUS_SUCCESS;
    PPRIVILEGE_SET Privileges = NULL;
    ACCESS_MASK GrantedAccess;

    //
    // See if the user has DELETE access to the target.
    //
    SeCaptureSubjectContext( &amp;SubjectContext );

    SeLockSubjectContext( &amp;SubjectContext );

    Granted = SeAccessCheck(targetSD,           // Target&#39;s SD.
                            &amp;SubjectContext,    // Captured security context.
                            TRUE,               // Tokens are locked.
                            DELETE,             // we only care about delete 
                            0,                  // previously granted access.
                            &amp;Privileges,        // privilege_set
                            IoGetFileObjectGenericMapping(), // Generic mappings.
                            UserMode,           // Mode
                            &amp;GrantedAccess,     // Granted access mask
                            &amp;status );          // Error code

    //
    // Do not need privilege set, so release it.
    //
    if (Privileges != NULL) { 

        SeFreePrivileges( Privileges ); 
        Privileges = NULL;
    }

    if (!Granted) {

        status = STATUS_SUCCESS;

        //
        // The user does not have DELETE access to the target, but 
        // could have FILE_DELETE_CHILD access to the parent directory.
        //
        (void) FsdLoadSecurityDescriptor(IrpContext, ParentFcb);
        if (!ParentFcb->SecurityDescriptor) {
            //
            // fine - no security is fine - he gets to do what he wants 
            //
            SeUnlockSubjectContext( &amp;SubjectContext );
            SeReleaseSubjectContext( &amp;SubjectContext );
            return STATUS_SUCCESS;
        }

 
        Granted = SeAccessCheck(&amp;ParentFcb->SecurityDescriptor,
                                &amp;SubjectContext,   // Captured security context.
                                TRUE,              // Tokens are locked.
                                FILE_DELETE_CHILD, // we only care about delete 
                                0,                 // Previously granted access.
                                &amp;Privileges,       // privilege_set
                                IoGetFileObjectGenericMapping(), // Generic mappings
                                UserMode,          // mode
                                &amp;GrantedAccess,    // Granted access mask
                                &amp;status );         // Error code
        //
        // Release privileges
        //
        if (Privileges != NULL) { 
            SeFreePrivileges( Privileges ); 
            Privileges = NULL;
        }
    }
    SeUnlockSubjectContext( &amp;SubjectContext );
    SeReleaseSubjectContext( &amp;SubjectContext );
    return status;
}
```

This code can be used for both the rename and hard link creation case.

Note that it is outside the scope of this document to discuss policy level code where the file system decides to disallow the delete based upon the type of file being deleted.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[ifsk\ifsk]:%20IRP_MJ_SET_INFORMATION%20%20RELEASE:%20%285/9/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


