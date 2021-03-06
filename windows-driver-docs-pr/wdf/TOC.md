# [WDF Driver Development Guide](index.md)
## [What's New for  WDF Drivers](what-s-new-for-wdf-drivers.md)
## [WDF Architecture](kernel-mode-driver-framework-architecture.md)
## [Getting Started with UMDF](getting-started-with-umdf-version-2.md)
### [User-Mode Driver Framework Frequently Asked Questions](user-mode-driver-framework-frequently-asked-questions.md)
### [Advantages of Writing UMDF Drivers](advantages-of-writing-umdf-drivers.md)
### [Overview of UMDF](overview-of-the-umdf.md)
### [UMDF Driver Host Process](umdf-driver-host-process.md)
### [Architecture of UMDF](detailed-view-of-the-umdf-architecture.md)
### [Comparing UMDF 2.0 Functionality to KMDF](comparing-umdf-2-0-functionality-to-kmdf.md)
### [How to convert a KMDF driver to a UMDF 2.0 driver (and vice-versa)](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)
### [Porting a Driver from UMDF 1 to UMDF 2](porting-a-driver-from-umdf-1-to-umdf-2.md)
## [Writing a Simple WDF Driver](writing-a-simple-kmdf-driver.md)
## [Using WDF to Develop a Driver](using-the-framework-to-develop-a-driver.md)
## [Framework Library Versioning](framework-library-versioning.md)
## [KMDF Version History](kmdf-version-history.md)
## [UMDF Version History](umdf-version-history.md)
## [Sample KMDF Drivers](sample-kmdf-drivers.md)
## [Sample UMDF Drivers](sample-umdf-drivers.md)
## [Sample Toaster Driver Programming Tour](sample-toaster-driver-programming-tour.md)
## [Developing Drivers with the Windows Driver Foundation: Reference Book](developing-drivers-with-wdf.md)
## [WDF Objects](wdf-objects.md)
### [Introduction to Framework Objects](introduction-to-framework-objects.md)
### [Framework Object Methods](framework-object-methods.md)
### [Framework Object Events](framework-object-events.md)
### [Framework Object Properties](framework-object-properties.md)
### [Framework Object Life Cycle](framework-object-life-cycle.md)
### [Framework Object Context Space](framework-object-context-space.md)
### [Framework Object Custom Types](framework-object-custom-types.md)
### [Using General Framework Objects](using-general-framework-objects.md)
### [Framework Object Collections](framework-object-collections.md)
### [Summary of Framework Objects](summary-of-framework-objects.md)
### [Framework Object Creation Errors](framework-object-creation-errors.md)
## [PnP and Power Management](pnp-and-power-management.md)
### [Introduction](introduction.md)
### [Supporting PnP and Power Management in Your Driver](supporting-pnp-and-power-management-in-your-driver.md)
#### [Supporting PnP and Power Management in Software-only Drivers](supporting-pnp-and-power-management-in-software-only-drivers.md)
#### [Supporting PnP and Power Management in Function Drivers](supporting-pnp-and-power-management-in-function-drivers.md)
### [Creating a Framework Device Object](creating-a-framework-device-object.md)
#### [Creating Device Objects in a Function Driver](creating-device-objects-in-a-function-driver.md)
#### [Creating Device Objects in a Filter Driver](creating-device-objects-in-a-filter-driver.md)
#### [Creating Device Objects in a Bus Driver](creating-device-objects-in-a-bus-driver.md)
### [Power Policy Ownership](power-policy-ownership.md)
#### [Supporting Idle Power-Down](supporting-idle-power-down.md)
#### [Supporting System Wake-Up](supporting-system-wake-up.md)
#### [User Control of Device Idle and Wake Behavior](user-control-of-device-idle-and-wake-behavior.md)
#### [Supporting Functional Power States](supporting-functional-power-states.md)
##### [Supporting Single-Component Devices with Single or Multiple Functional Power States](supporting-multiple-functional-power-states-for-single-component-devices.md)
##### [Supporting Multiple-Component Devices with Single or Multiple Functional Power States](supporting-multiple-functional-power-states-for-multiple-component-devices.md)
###### [Coordinating I/O Requests with Component Power State](coordinating-i-o-requests-with-component-power-state.md)
###### [Reporting Device Powered On When System Returns to S0](reporting-device-powered-on.md)
###### [Supporting Idle Power-Down on Multiple-Component Devices](supporting-idle-power-down-on-multiple-component-devices.md)
### [Power Management for I/O Queues](power-management-for-i-o-queues.md)
### [Using Self-Managed I/O](using-self-managed-i-o.md)
### [Handling Requests to Stop a Device](handling-requests-to-stop-a-device.md)
### [PnP and Power Management Scenarios](pnp-and-power-management-scenarios.md)
#### [A User Plugs in a Device](a-user-plugs-in-a-device.md)
#### [A User Unplugs a Device](a-user-unplugs-a-device.md)
#### [A Device Enters a Low-Power State](a-device-enters-a-low-power-state.md)
#### [A Device Returns to Its Working State](a-device-returns-to-its-working-state.md)
#### [The PnP Manager Redistributes System Resources](the-pnp-manager-redistributes-system-resources.md)
### [PnP and Power Management Callback Sequences](pnp-and-power-management-callback-sequences.md)
#### [Power-Up Sequence for a Function or Filter Driver](power-up-sequence-for-a-function-or-filter-driver.md)
#### [Power-Up Sequence for a Bus Driver](power-up-sequence-for-a-bus-driver.md)
#### [Power-Down and Removal Sequence for a Function or Filter Driver](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
#### [Power-Down and Removal Sequence for a Bus Driver](power-down-and-removal-sequence-for-a-bus-driver.md)
#### [Surprise-Removal Sequence](surprise-removal-sequence.md)
### [Driver Access to Hardware](driver-access-to-hardware.md)
### [Reporting Device Failures](reporting-device-failures.md)
## [Handling I/O Requests](handling-i-o-requests-in-wdf-drivers.md)
### [Creating WDF HID Minidrivers](creating-umdf-hid-minidrivers.md)
### [Framework File Objects](framework-file-objects.md)
### [Framework Queue Objects](framework-queue-objects.md)
#### [Creating I/O Queues](creating-i-o-queues.md)
##### [Dispatching Methods for I/O Requests](dispatching-methods-for-i-o-requests.md)
##### [Request Handlers](request-handlers.md)
#### [Deleting I/O Queues](deleting-i-o-queues.md)
#### [Managing I/O Queues](managing-i-o-queues.md)
#### [Using Power-Managed I/O Queues](using-power-managed-i-o-queues.md)
#### [I/O Queue States](i-o-queue-states.md)
#### [Example Uses of I/O Queues](example-uses-of-i-o-queues.md)
### [Framework Request Objects](framework-request-objects.md)
#### [Creating Framework Request Objects](creating-framework-request-objects.md)
#### [Using Request Object Context](using-request-object-context.md)
#### [Request Ownership](request-ownership.md)
#### [Processing I/O Requests](processing-i-o-requests.md)
##### [Receiving I/O Requests](receiving-i-o-requests.md)
##### [Requeuing I/O Requests](requeuing-i-o-requests.md)
##### [Completing I/O Requests](completing-i-o-requests.md)
##### [Canceling I/O Requests](canceling-i-o-requests.md)
###### [Synchronizing Cancel and Completion Code](synchronizing-cancel-and-completion-code.md)
###### [Synchronizing Cancellation of Sent Requests](synchronizing-cancellation-of-sent-requests.md)
##### [Forwarding I/O Requests](forwarding-i-o-requests.md)
#### [Obtaining Information About an I/O Request](obtaining-information-about-an-i-o-request.md)
#### [Accessing Data Buffers in WDF Drivers (KMDF or UMDF)](accessing-data-buffers-in-wdf-drivers.md)
#### [Managing Buffer Access Methods in UMDF Drivers](managing-buffer-access-methods-in-umdf-drivers.md)
#### [Reusing Framework Request Objects](reusing-framework-request-objects.md)
### [Handling Client Impersonation in UMDF Drivers](handling-client-impersonation-in-umdf-drivers.md)
### [Host Process Timeouts in UMDF](how-umdf-enforces-time-outs.md)
### [Supporting Kernel-Mode Clients in UMDF Drivers](supporting-kernel-mode-clients-in-umdf-drivers.md)
### [Using Activity Identifiers](using-activity-identifiers.md)
## [Using I/O Targets](using-i-o-targets.md)
### [Introduction to I/O Targets](introduction-to-i-o-targets.md)
### [General I/O Targets](general-i-o-targets.md)
#### [Initializing a General I/O Target](initializing-a-general-i-o-target.md)
#### [Sending I/O Requests to General I/O Targets](sending-i-o-requests-to-general-i-o-targets.md)
##### [Sending I/O Requests Synchronously](sending-i-o-requests-synchronously.md)
##### [Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md)
#### [Controlling a General I/O Target's State](controlling-a-general-i-o-target-s-state.md)
#### [Obtaining Information About a General I/O Target](obtaining-information-about-a-general-i-o-target.md)
### [USB I/O Targets](usb-i-o-targets.md)
#### [Working with USB Devices](working-with-usb-devices.md)
#### [Working with USB Interfaces](working-with-usb-interfaces.md)
#### [Working with USB Pipes](working-with-usb-pipes.md)
## [Synchronization Techniques](synchronization-techniques-for-wdf-drivers.md)
### [Using Automatic Synchronization](using-automatic-synchronization.md)
### [Using Framework Locks](using-framework-locks.md)
## [WDF Support Objects](wdf-support-objects.md)
### [Using Memory Buffers](using-memory-buffers.md)
### [Memory Buffer Life Cycle](memory-buffer-life-cycle.md)
### [Using Timers](using-timers.md)
### [Using String Objects](using-string-objects.md)
### [Using Framework Work Items](using-framework-work-items.md)
### [Using Device Interfaces](using-device-interfaces.md)
### [Using the Registry in WDF Drivers](using-the-registry-in-wdf-drivers.md)
#### [Introduction to Registry Keys for Drivers](introduction-to-registry-keys-for-drivers.md)
#### [Using Framework Registry-Key Objects](using-framework-registry-key-objects.md)
#### [Accessing the Unified Device Property Model](accessing-the-unified-device-property-model.md)
### [Security Issues for KMDF Drivers](security-issues-for-kmdf-drivers.md)
#### [Controlling Device Access in KMDF Drivers](controlling-device-access-in-kmdf-drivers.md)
## [Handling Hardware Interrupts](handling-hardware-interrupts.md)
### [Creating an Interrupt Object](creating-an-interrupt-object.md)
### [Enabling and Disabling Interrupts](enabling-and-disabling-interrupts.md)
### [Servicing an Interrupt](servicing-an-interrupt.md)
### [Synchronizing Interrupt Code](synchronizing-interrupt-code.md)
### [Supporting Passive-Level Interrupts](supporting-passive-level-interrupts.md)
### [Using an Interrupt to Wake a Device](using-an-interrupt-to-wake-a-device.md)
### [Handling Active-Both Interrupts](handling-active-both-interrupts.md)
## [Handling DMA Operations in KMDF Drivers](handling-dma-operations-in-kmdf-drivers.md)
### [Introduction to DMA in Windows Driver Framework](introduction-to-dma-in-windows-driver-framework.md)
### [Framework DMA Objects](framework-dma-objects.md)
### [DMA Transactions and DMA Transfers](dma-transactions-and-dma-transfers.md)
### [Sample Drivers That Use Framework DMA](sample-drivers-that-use-framework-dma.md)
### [Handling I/O Requests in a KMDF Driver for a Bus-Master DMA Device](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)
#### [Enabling DMA Transactions](enabling-dma-transactions.md)
#### [Creating and Initializing a DMA Transaction](creating-and-initializing-a-dma-transaction.md)
#### [Starting a DMA Transaction](starting-a-dma-transaction.md)
#### [Programming DMA Hardware](programming-dma-hardware.md)
#### [Completing a DMA Transfer](completing-a-dma-transfer.md)
#### [Completing a DMA Transaction](completing-a-dma-transaction.md)
#### [Reusing DMA Transaction Objects](reusing-dma-transaction-objects.md)
#### [Supporting Power Management for DMA Devices](supporting-power-management-for-dma-devices.md)
#### [Using Common Buffers](using-common-buffers.md)
### [Supporting System-Mode DMA](supporting-system-mode-dma.md)
### [Canceling DMA Transactions](canceling-dma-transactions.md)
### [Reserving DMA Resources](reserving-dma-resources.md)
### [Testing DMA in KMDF Drivers](testing-dma-in-kmdf-drivers.md)
## [Supporting WMI in KMDF Drivers](supporting-wmi-in-kmdf-drivers.md)
### [Introduction to WMI for KMDF Drivers](introduction-to-wmi-for-kmdf-drivers.md)
### [Initializing WMI Support in Your Driver](initializing-wmi-support-in-your-driver.md)
### [Supporting WMI Data Blocks and Events in Your Driver](supporting-wmi-data-blocks-and-events-in-your-driver.md)
## [Accessing WDM Interfaces in KMDF Drivers](accessing-wdm-interfaces-in-kmdf-drivers.md)
### [Obtaining WDM Information](obtaining-wdm-information.md)
### [Handling WDM IRPs Outside of the Framework](handling-wdm-irps-outside-of-the-framework.md)
#### [Handling an IRP that the Framework Does Not Support](handling-an-irp-that-the-framework-does-not-support.md)
#### [Preprocessing and Postprocessing IRPs](preprocessing-and-postprocessing-irps.md)
#### [Dispatching IRPs to I/O Queues](dispatching-irps-to-i-o-queues.md)
### [WDM Interface Restrictions](wdm-interface-restrictions.md)
## [Handling Hardware Resources](hardware-resources-for-kmdf-drivers.md)
### [Introduction to Hardware Resources](introduction-to-hardware-resources.md)
### [Framework Objects for Hardware Resources](framework-objects-for-hardware-resources.md)
### [Creating a Resource Requirements List](creating-a-resource-requirements-list.md)
### [Modifying a Resource Requirements List](modifying-a-resource-requirements-list.md)
### [Creating a Resource List for a Boot Configuration](creating-a-resource-list-for-a-boot-configuration.md)
### [Modifying a Resource List](modifying-a-resource-list.md)
### [Raw and Translated Resources](raw-and-translated-resources.md)
### [Finding and Mapping Hardware Resources](finding-and-mapping-hardware-resources.md)
### [Reading and Writing to Device Registers](reading-and-writing-to-device-registers.md)
## [Building, Installing, and Testing](building--installing--and-testing-a-wdf-driver.md)
### [Building and Loading a WDF Driver](building-and-loading-a-kmdf-driver.md)
### [Redistributable Framework Components](installation-components-for-kmdf-drivers.md)
### [Specifying the  KMDF Co-installer in an INF File](installing-the-framework-s-co-installer.md)
### [Using the UMDF Co-installer](using-the-umdf-co-installer.md)
### [Using INX Files to Create INF Files](using-inx-files-to-create-inf-files.md)
### [Testing a WDF Driver (KMDF or UMDF)](testing-a-kmdf-driver.md)
### [Troubleshooting KMDF and UMDF Driver Installation](debugging-driver-installation.md)
### [Installing a UMDF Filter Driver](installing-a-umdf-filter-driver.md)
### [Specifying  the Reflector in an INF File](adding-the-reflector.md)
### [Specifying WDF Directives in INF Files](specifying-wdf-directives-in-inf-files.md)
### [Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)
### [Session Zero Guidelines for UMDF Drivers](session-zero-guidelines-for-umdf-drivers.md)
### [Restricting the Loading Location of UMDF Drivers](restricting-the-loading-location-of-umdf-drivers.md)
### [Controlling Device Access](controlling-device-access.md)
### [Using the Framework's Event Logger](using-the-framework-s-event-logger.md)
### [Using KMDF Verifier](using-kmdf-verifier.md)
### [Using UMDF Verifier](using-umdf-verifier.md)
### [How UMDF Handles Driver Failures](how-umdf-handles-driver-failures.md)
### [How UMDF Handles Application Failures](how-umdf-handles-application-failures.md)
### [How UMDF Reports Errors](how-umdf-reports-errors.md)
## [Debugging WDF Drivers](debugging-a-wdf-driver.md)
### [Accessing UMDF Metadata in WER Reports](accessing-umdf-metadata-in-wer-reports.md)
### [Attaching a User-Mode Debugger](attaching-a-user-mode-debugger.md)
### [Avoiding Reboot when Updating a UMDF Driver](avoiding-reboot-when-updating-a-umdf-driver.md)
### [Breaking into a Debugger from KMDF Drivers](breaking-into-a-debugger-from-kmdf-drivers.md)
### [Bug Checks from KMDF Drivers](bug-checks-from-kmdf-drivers.md)
### [Debugging Power Reference Leaks in WDF](debugging-power-reference-leaks-in-wdf.md)
### [Determining If a Driver Leaks Framework Objects](determining-if-a-driver-leaks-framework-objects.md)
### [Determining the State of a UMDF Device](determining-the-state-of-a-umdf-device.md)
### [Determining Why an Application Request Does Not Complete](determining-why-an-application-request-does-not-complete.md)
### [Determining Why the Reflector Terminated the Host Process](determining-why-the-reflector-terminated-the-host-process.md)
### [Determining Why the UMDF Driver Fails to Load or the UMDF Device Fails to Start](determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails.md)
### [Determining Why UMDF Indicates Outstanding Files at Device Removal Time](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)
### [How to Enable Debugging of a UMDF Driver](enabling-a-debugger.md)
### [Registry Values for Debugging WDF Drivers (KMDF and UMDF)](registry-values-for-debugging-kmdf-drivers.md)
### [Summary of Debugger Extensions in Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md)
### [Troubleshooting UMDF 2.0 Driver Crashes](debugging-umdf-2-0-drivers.md)
### [Using Inflight Trace Recorder (IFR) in KMDF and UMDF 2 Drivers](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)
### [Using the Windows Performance Toolkit (WPT) with WDF](using-the-windows-performance-toolkit--wpt--with-wdf.md)
### [Using WPP Software Tracing in KMDF Drivers](using-wpp-software-tracing-in-kmdf-drivers.md)
### [Using WPP Software Tracing in UMDF Drivers](using-wpp-software-tracing-in-umdf-drivers.md)
### [Video: Debugging your driver with WDF source code](video--debugging-your-driver-with-wdf-source-code.md)
### [Videos: Debugging KMDF Drivers](debugging-kernel-mode-driver-framework-drivers.md)
### [Videos: Debugging UMDF Drivers](videos--debugging-umdf-drivers.md)
## [Porting a Driver from WDM to WDF](wdf-porting-guide.md)
### [Which Drivers Can Be Ported and Where](which-drivers-can-be-ported.md)
### [WDM Concepts for WDF Drivers](wdm-concepts-for-kmdf-drivers.md)
### [Differences Between WDM and WDF](differences-between-wdm-and-kmdf.md)
### [Preparing for Porting](general-guidelines-for-porting.md)
### [Steps in Porting](how-to-port.md)
#### [Porting DriverEntry](porting-driver-entry.md)
#### [Porting AddDevice to EvtDriverDeviceAdd](porting-adddevice-to-evtdriverdeviceadd.md)
#### [Porting Interrupts](porting-interrupt-functionality.md)
#### [Porting PnP and Power Management](porting-pnp-and-power-management-functionality.md)
#### [Porting I/O](porting-i-o-handling.md)
##### [Porting I/O Queues](porting-i-o-queues.md)
##### [Porting I/O Dispatch Routines to I/O Event Callback Functions](porting-i-o-dispatch-routines-to-i-o-event-callback-functions.md)
##### [Revise Code That Handles Completed Requests](revise-completed-request-logic.md)
##### [Revise Canceled Request Logic](revise-canceled-request-logic.md)
##### [Revise Forward Request Logic](revise-forward-request-logic.md)
##### [Revise Code That Issues I/O Requests](revise-code-that-issues-i-o-requests.md)
#### [Porting DMA](porting-dma.md)
#### [Porting WMI](porting-wmi-code.md)
#### [Requests That KMDF Does Not Support](requests-that-kmdf-does-not-support.md)
#### [Installation Procedure](installation-procedure.md)
### [Summary of KMDF and WDM Equivalents](summary-of-kmdf-and-wdm-equivalents.md)
#### [WDM Equivalents for WDF Buffer Pointers](wdm-equivalents-for-kmdf-buffer-pointers.md)
#### [WDM IRPs and WDF Event Callback Functions](wdm-irps-and-kmdf-event-callback-functions.md)
## [Additional Topics for KMDF Drivers](kmdf-only-functionality.md)
### [Using Kernel-Mode Driver Framework with Non-PnP Drivers](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)
### [Installing a Non-PnP Driver](installing-a-non-pnp-driver.md)
### [Guaranteeing Forward Progress of I/O Operations](guaranteeing-forward-progress-of-i-o-operations.md)
### [Specifying Priority Boosts When Completing I/O Requests](specifying-priority-boosts-when-completing-i-o-requests.md)
### [Supporting PnP and Power Management in Bus Drivers](supporting-pnp-and-power-management-in-bus-drivers.md)
### [Enumerating the Devices on a Bus](enumerating-the-devices-on-a-bus.md)
#### [Static Enumeration](static-enumeration.md)
#### [Dynamic Enumeration](dynamic-enumeration.md)
#### [Handling Enumeration Requests](handling-enumeration-requests.md)
### [Supporting Ejectable Devices](supporting-ejectable-devices.md)
### [State Machines in the Framework](state-machines-in-the-framework.md)
### [Using Driver-Defined Interfaces](using-driver-defined-interfaces.md)
### [Supporting Special Files](supporting-special-files.md)
### [Using Control Device Objects](using-control-device-objects.md)
### [Creating KMDF Miniport Drivers](creating-kmdf-miniport-drivers.md)
### [Creating Pageable Code in a KMDF Driver](creating-pageable-code-in-a-kmdf-driver.md)
## [UMDF 1.x Design Guide](user-mode-driver-framework-design-guide.md)
### [UMDF Objects and Interfaces](umdf-objects-and-interfaces.md)
#### [Framework Objects](framework-objects.md)
##### [Framework Base Object](framework-base-object.md)
##### [Framework Driver Object](framework-driver-object.md)
##### [Framework Device Object](framework-device-object.md)
##### [Framework File Object](framework-file-object.md)
##### [Framework I/O Queue Object](framework-i-o-queue-object.md)
##### [Framework I/O Request Object](framework-i-o-request-object.md)
##### [Framework I/O Target Object](framework-i-o-target-object.md)
##### [Framework Interrupt Object](framework-interrupt-object.md)
##### [Framework Memory Object](framework-memory-object.md)
#### [Framework Object Hierarchy](framework-object-hierarchy.md)
#### [UMDF Based on COM Subset](umdf-based-on-com-subset.md)
#### [UMDF DDI Programming Model](umdf-ddi-programming-model.md)
#### [Managing the Lifetime of Objects](managing-the-lifetime-of-objects.md)
### [Initializing UMDF Drivers](initializing-umdf-drivers.md)
#### [Adding a Device Overview](adding-a-device-overview.md)
#### [Adding a Device](adding-a-device.md)
### [PnP and Power Management in UMDF Drivers](pnp-and-power-management-in-umdf-drivers.md)
#### [PnP and Power Management Interfaces](pnp-and-power-management-interfaces.md)
#### [Power Policy Ownership in UMDF](power-policy-ownership-in-umdf.md)
##### [Supporting Idle Power-Down in UMDF Drivers](supporting-idle-power-down-in-umdf-drivers.md)
##### [Supporting System Wake-Up in UMDF Drivers](supporting-system-wake-up-in-umdf-drivers.md)
##### [User Control of Device Idle and Wake Behavior in UMDF](user-control-of-device-idle-and-wake-behavior-in-umdf.md)
#### [PnP and Power Management Scenarios in UMDF](pnp-and-power-management-scenarios-in-umdf.md)
##### [A User Plugs in a Device](a-user-plugs-in-a-device-umdf.md)
##### [A User Unplugs a Device](a-user-unplugs-a-device-umdf.md)
##### [A Device Enters a Low-Power State](a-device-enters-a-low-power-state-umdf.md)
##### [A Device Returns to Its Working State](a-device-returns-to-its-working-state-umdf.md)
##### [The PnP Manager Redistributes System Resources](the-pnp-manager-redistributes-system-resources-umdf.md)
### [Processing I/O Requests](processing-i-o-requests-umdf.md)
#### [I/O Request Processing Operation Flow](i-o-request-processing-operation-flow.md)
##### [Operation Flow with Single Device Stack](operation-flow-with-single-device-stack.md)
##### [Operation Flow with Double Device Stack](operation-flow-with-double-device-stack.md)
#### [Sending I/O Requests to Lower Drivers](sending-i-o-requests-to-lower-drivers.md)
#### [Obtaining Parameters for I/O Requests](obtaining-parameters-for-i-o-requests.md)
#### [Canceling I/O Requests](canceling-i-o-requests-umdf.md)
#### [Completing I/O Requests](completing-i-o-requests-umdf.md)
#### [Accessing Data Buffers in UMDF Drivers](accessing-data-buffers-in-umdf-1-x-drivers.md)
#### [Reusing Framework Request Objects](reusing-framework-request-objects-umdf.md)
#### [Handling Client Impersonation in UMDF 1.x Drivers](handling-client-impersonation-in-umdf-1-x-drivers.md)
#### [Preventing an Imbalance of Create and Close Notifications to a Driver](preventing-an-imbalance-of-create-and-close-notifications-to-a-driver.md)
### [Using I/O Targets in UMDF](using-i-o-targets-in-umdf.md)
#### [General I/O Targets in UMDF](general-i-o-targets-in-umdf.md)
##### [Initializing a General I/O Target in UMDF](initializing-a-general-i-o-target-in-umdf.md)
##### [Sending I/O Requests to a General I/O Target in UMDF](sending-i-o-requests-to-a-general-i-o-target-in-umdf.md)
##### [Controlling a General I/O Target's State in UMDF](controlling-a-general-i-o-target-s-state-in-umdf.md)
##### [Obtaining Information About a General I/O Target in UMDF](obtaining-information-about-a-general-i-o-target-in-umdf.md)
#### [USB I/O Targets in UMDF](usb-i-o-targets-in-umdf.md)
##### [Choosing a Driver Model for a USB Device](choosing-a-driver-model-for-a-usb-device.md)
##### [USB-Specific UMDF 1.x Interfaces](usb-specific-umdf-1-x-interfaces.md)
##### [Working with USB Devices in UMDF 1.x Drivers](working-with-usb-devices-in-umdf-1-x-drivers.md)
##### [Working with USB Interfaces in UMDF 1.x Drivers](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
##### [Working with USB Pipes in UMDF 1.x Drivers](working-with-usb-pipes-in-umdf-1-x-drivers.md)
##### [File Creation by a USB I/O Target](file-creation-by-a-usb-i-o-target.md)
##### [Calling WinUSB from UMDF](escaping-to-winusb.md)
### [Accessing Hardware and Handling Interrupts](accessing-hardware-and-handling-interrupts.md)
#### [Enabling Hardware Access](enabling-hardware-access.md)
#### [Finding and Mapping Hardware Resources in UMDF 1.x Drivers](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)
#### [Reading and Writing to Device Registers in UMDF 1.x Drivers](reading-and-writing-to-device-registers-in-umdf-1-x-drivers.md)
#### [Handling Interrupts](handling-interrupts.md)
##### [Creating an Interrupt Object](creating-an-interrupt-object-umdf.md)
##### [Enabling and Disabling Interrupts](enabling-and-disabling-interrupts-umdf.md)
##### [Servicing an Interrupt](servicing-an-interrupt-umdf.md)
##### [Using Work Items](using-workitems.md)
##### [Synchronizing Interrupt Code](synchronizing-interrupt-code-umdf.md)
##### [Deleting an Interrupt Object](deleting-an-interrupt-object.md)
### [UMDF Driver Tasks](umdf-driver-tasks.md)
#### [Using Device Interfaces in UMDF Drivers](using-device-interfaces-in-umdf-drivers.md)
#### [Creating Callback Objects](creating-callback-objects.md)
##### [Creating Callback Objects Example](creating-callback-objects-example.md)
##### [Defining Callback Objects Example](defining-callback-objects-example.md)
##### [Associating Callback Interfaces Example](associating-callback-interfaces-example.md)
#### [Specifying a Callback Synchronization Mode](specifying-a-callback-synchronization-mode.md)
#### [I/O Queue Event Callback Functions](i-o-queue-event-callback-functions.md)
#### [Configuring Dispatch Mode for an I/O Queue](configuring-dispatch-mode-for-an-i-o-queue.md)
#### [Combining Dispatch and Synchronization Modes](combining-dispatch-and-synchronization-modes.md)
#### [Creating a File Object to Handle I/O](creating-a-file-object-to-handle-i-o.md)
##### [Driver-Created Versus Application-Created File Objects](driver-created-versus-application-created-file-objects.md)
##### [Creating and Using Driver-Created File Objects](creating-and-using-driver-created-file-objects.md)
#### [Using the Registry in UMDF 1.x Drivers](using-the-registry-in-umdf-1-x-drivers.md)
#### [Supporting Kernel-Mode Clients in UMDF 1.x Drivers](supporting-kernel-mode-clients-in-umdf-1-x-drivers.md)
#### [Viewing UMDF Objects](viewing-umdf-objects.md)
#### [Determining Why a UMDF Driver Consumes an Excessive Amount of Memory](determining-why-a-umdf-driver-consumes-an-excessive-amount-of-memory.md)
#### [Summary of Debugger Extensions in Wudfext.dll](using-umdf-debugger-extensions.md)

