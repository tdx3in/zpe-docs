---
title: Nodegrid Manager installation on Linux Qemu/KVM 
date: 2017-01-05
weight: 1  
description: >
  This documentation details steps to create a Nodegrid Manager VM instance on Linux Qemu/KVM.
categories: [installation]
tags: [installation, linux, docs]
---



<p data-block-id="20d0ae8a-99e3-4fc0-a2c0-9d803e46a9f8"></p>
<p data-block-id="0bc17893-bf20-472b-afb7-cc7ac384696b">Kernel-based Virtual Machine (KVM) is a full virtualization
    solution for Linux on x86 hardware with virtualization extensions support (e.g., Intel VT or AMD-V). It consists of
    a loadable kernel module on the host (kvm.co) that provides core virtualization infrastructure and a
    processor-specific module (e.g., kvm-intel.ko or kvm-amd.ko).</p>
<p data-block-id="7ed7c482-7a7a-4e35-a11f-3f20f696b99c">KVM is a type 1 hypervisor (i.e., bare metal hypervisor) and
    enables the definition of virtual machines (VM guests). Each VM has private virtualized hardware like a network
    card, disk, graphics adapter, serial ports, and others.</p>
<blockquote data-block-id="f5c5e92b-eeab-448e-984c-62b6ea75f22b" style="overflow:auto;">
    <p data-block-id="b11638ae-acf0-49cc-bae7-6f4837be24c0">The kernel component of KVM is included in mainline Linux,
        as of 2.6.20. The user space component of KVM is included in mainline QEMU, as of 1.3.</p>
</blockquote>
<p data-block-id="be3bec34-e88e-4915-98fc-c98d5252d98f">The following diagram, Diagram-1, depicts the expected
    result:<br type="inline"><img data-block-id="6de3fc4f-b4ed-48ac-bd5c-926861a1c7cc"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/image-4CEFY1CI.png"
        alt="image.png" width="400" type="inline-block" fixaspectratio="false" mediatype="inline-block-img"
        autoaspectratio="false" shadow="no" border="no" round="no" heightauto="true" widthauto="false" style=""></p>
<p data-block-id="64dfdd8b-47b9-47f7-a43e-9c6dc637e343">This guide structure is as follows:</p>
<ol data-block-id="83916736-114f-4976-aef1-82568f02914e">
    <li data-block-id="854ab6bf-2014-488f-9577-d25977474df7">
        <p data-block-id="8b3e3db6-98e7-4d17-b927-522db8594cb0">Linux Host requirements</p>
    </li>
    <li data-block-id="b4ed4bb8-e88d-49e7-8586-1f76a375fe25">
        <p data-block-id="b804dcb9-c296-4634-a957-d8c919117d75">Nodegrid Manager ISO image</p>
    </li>
    <li data-block-id="fe6520fa-fe58-4ff0-bc7c-4a72cf046add">
        <p data-block-id="c062c6d1-9a5c-41c3-8128-efe50dd15f39">Create a Nodegrid Manager instance</p>
    </li>
    <li data-block-id="c3389e85-4b27-41ac-9855-32956e760e16">
        <p data-block-id="f8726c09-f663-4e98-a2a4-1e8b5363813f">Web Access to the Nodegrid Manager</p>
    </li>
</ol>

## Linux Host requirements
<p data-block-id="535b1d19-7836-41f0-8f95-e435d2a8f535">The requirements for Linux Qemu/KVM include:</p>
<ul data-block-id="528d800e-b51d-43fd-91fa-9e680544d41c">
    <li data-block-id="52e5d7ca-7598-4511-9151-d515a2fa998c">
        <p data-block-id="85152ffd-7993-4495-987d-68999585b14c">Hardware:</p>
        <ul data-block-id="b693e025-c56c-445c-9df9-dd8ab33e4c3c">
            <li data-block-id="d50a9c99-3d03-4680-94ca-a0bb53352669">
                <p data-block-id="7a067f10-bad6-4d33-aae2-d723d6cc3e4c">Virtualization Technologies for x86 (AMD-V /
                    Intel VT)</p>
            </li>
        </ul>
    </li>
    <li data-block-id="0d97b9a9-a0a8-47b0-a4e8-9aa76294a215">
        <p data-block-id="1913680b-ca71-48e6-ba69-b9273a601daf">Software:</p>
        <ul data-block-id="db2f411f-57c8-49dd-8d85-bc8a4d9cad35">
            <li data-block-id="8e378cd4-3c7e-4a87-af74-20c9a8bcdda6">
                <p data-block-id="c9f02afb-5526-4b00-9ef3-265f993c4b6b">Linux kernel 2.6.20 or newer</p>
            </li>
            <li data-block-id="175fba7c-4416-4b69-a15b-f4b992dce3e1">
                <p data-block-id="1e652ff9-2921-4143-a10b-15e7e3676eed">QEMU 1.3 or newer</p>
            </li>
        </ul>
    </li>
</ul>
<p data-block-id="4b96da9c-a09f-4c15-80fe-ffeaf5198a94">This guide consider the following software:</p>
<ul data-block-id="ecf916df-3bad-4116-8462-c173a9569100">
    <li data-block-id="b099e44f-08ce-4562-b95b-2d0fc2a2cbd0">
        <p data-block-id="f061dc1a-7d71-42a7-bc90-70fc912e1da4">OS: <a
                href="https://www.debian.org/releases/bullseye/">Debian 11 <em>bullseye</em></a></p>
    </li>
    <li data-block-id="e71b5599-8eba-4818-a624-c9c309250b7b">
        <p data-block-id="f1ff10e7-c0bc-4401-ba6a-957cd5153826"><a href="https://libvirt.org/">Libvirt</a>, the
            virtualization API </p>
        <blockquote data-block-id="0abf1569-3dff-4aed-aaca-6f42c9f6446d" style="overflow:auto;">
            <p data-block-id="cf4c6497-2ddb-429b-8eb7-de059539552c">libvirt is an open-source API, daemon and management
                tool for managing platform virtualization.</p>
        </blockquote>
    </li>
    <li data-block-id="57fb74b7-46ea-49b2-aa0b-2dfc414a8a05">
        <p data-block-id="8edd0dcf-bc69-4cff-a56f-8a7226e21303">Virtual Machine Manager <a
                href="https://virt-manager.org/">virt-manager</a></p>
        <blockquote data-block-id="350a4086-4859-4024-b78e-00b6d5bb4343" style="overflow:auto;">
            <p data-block-id="4634d36b-4570-4521-a9fe-5aac14bc9f8d">The virt-manager application is a desktop user
                interface to manage virtual machines through libvirt.</p>
        </blockquote>
    </li>
</ul>
<blockquote data-block-id="573ecc31-4d2f-455e-a547-70279ddb6b10" style="overflow:auto;">
    <p data-block-id="15b28843-9c11-458a-8f59-78b6e9881d7e">NOTE: virt-manager is not required to be installed on the
        KVM hypervisor. It can be installed in a desktop, with <code>ssh</code> access to the KVM hypervisor.</p>
</blockquote>
<p data-block-id="7b64f6b5-d7a7-4044-9095-371043903c21">Here are further details about KVM installation on Debian 11 <a
        href="https://wiki.debian.org/KVM#Installation">https://wiki.debian.org/KVM</a>.</p>

## Nodegrid Manager ISO image
<p data-block-id="c35f95d7-75fb-41c5-a075-4563d117c06b">The following steps describe how to obtain a Nodegrid Manager
    ISO file:</p>
<ol data-block-id="7cda5dad-861b-4dd2-8380-f68c44f62494">
    <li data-block-id="1c25013b-c76e-488c-a0e5-2bfb08c349d0">
        <p data-block-id="5d7af289-046c-4fd3-8588-35415eaa46a8">Access with your credentials to <a
                href="https://zpecloud.com">https://zpecloud.com</a> or <a href="https://zpecloud.eu" target="_self"
                translate="no">https://zpecloud.eu</a> based on your region.</p>
    </li>
    <li data-block-id="2d469b1d-cbed-463a-95ef-434abb79656c">
        <p data-block-id="0e99743e-8055-41d4-b295-078e4b69aece">Go to <em>PROFILES :: SOFTWARE</em>.</p>
    </li>
    <li data-block-id="572c9031-f655-4831-9080-e2e619c233fb">
        <p data-block-id="60d476b0-0173-496f-8f61-e5af8ba980a5">Select a VSR Nodegrid version, e.g.,
            <em>Nodegrid_Platform_v5.8.2_20230114</em></p>
    </li>
    <li data-block-id="1d82a2c4-2c86-4fe2-b0d6-5a95bdc6e9be">
        <p data-block-id="e29b7ecc-15c4-4aaf-83d5-5dfbf0796519">Download the ISO file</p>
    </li>
</ol>
<blockquote data-block-id="a17eefa6-dd7b-47c4-a3e9-15fbc4114735" style="overflow:auto;">
    <p data-block-id="d0a5e305-03dc-4695-bc91-4a0787f4a5f5">NOTE: The iso file can be obtained through the support
        portal.</p>
</blockquote>

## Create a Nodegrid Manager instance
<p data-block-id="7884dd88-71ba-4d83-9c66-e8f6a1448b48">The following steps describe the procedure to deploy a VM
    instance using the <em>virt-manager</em> graphical interface. This creates the resources shown in the
    <em>Diagram-1</em>.</p>
<ol data-block-id="8342479a-4190-477a-9d60-4c3f77d5cecf">
    <li data-block-id="96080579-ad1d-4f98-ae75-ec6ac49eae6c">
        <p data-block-id="91eb160e-5953-4c23-be4d-3946d0720a8e">Open the application <em>virt-manager</em> (Virtual
            Machine Manager) on your desktop</p>
    </li>
    <li data-block-id="c9feae42-8961-4be7-9efc-32c41575500a">
        <p data-block-id="d554dcd4-1a93-43b9-bfde-0e9df72d82db">If the KVM hypervisor is installed on the same machine,
            skip to step 3. To access a remote KVM hypervisor via <code>ssh</code>: </p>
        <ul data-block-id="45d47ab0-fc82-49d3-8813-02a575a10ab6">
            <li data-block-id="3eb96f76-5d67-411f-85bd-8392e8e143bf">
                <p data-block-id="962b826d-9ab8-4a43-9fd1-5f3a7718c34f">Select <strong>File &gt; Add Connection</strong>
                </p>
            </li>
            <li data-block-id="a58ece2f-c079-47bb-b099-4a91f75050f8">
                <p data-block-id="c367dd10-8607-4a2a-8766-5706d1255305">Click <strong>Connect to remote host over
                        SSH</strong></p>
            </li>
            <li data-block-id="6338b779-6527-48df-81a9-d3f7b364d3b4">
                <p data-block-id="53e3e8bd-1916-41e2-b40d-43680b704e3a">Enter the credentials</p>
            </li>
            <li data-block-id="c5cad295-8a9f-4ae9-a0f2-cd13aff42a12">
                <p data-block-id="dbd0572a-63fb-456c-aea4-afa5496db2c6">Click <strong>Connect</strong></p>
            </li>
        </ul>
    </li>
    <li data-block-id="74ead708-d8f1-4174-bc9b-e654033bf26e">
        <p data-block-id="2caa3f79-d0d0-4860-9e95-ffd13d46cc53">Click <strong>Create a new virtual machine</strong>.</p>
    </li>
    <li data-block-id="32334b83-a589-4496-a340-c2d99a58da94">
        <p data-block-id="c85a1f19-61d8-4920-aed7-c9d7d7a2cc95">Click <strong>Local install media (ISO image or CDROM)
                &gt; Forward</strong></p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="5dc64b67-d42c-4c68-8f4a-87f8e61c1cbb"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-1.png"
        mediatype="img" alt="" width="400" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:400px;"></div>
<ol data-block-id="01fbdcb1-35e9-4749-b097-497b6b8f2b4b" start="5">
    <li data-block-id="2515b975-4d45-4e66-8c1b-ede41ce36987">
        <p data-block-id="9a1eca25-7a1a-4184-8f58-35c1f14508ca">On <strong>Choose ISO or CDROM install media</strong>,
            go to <strong>Browse &gt; Browse Local</strong> and locate the downloaded ISO file.</p>
    </li>
    <li data-block-id="88fc3e39-b1eb-498c-944b-fc2df1f640cd">
        <p data-block-id="f45e9335-eb77-4baf-84f3-5747d45e4320">On <strong>Choose the operating system to
                install</strong>, insert <em>Generic Linux 2022</em> (unselect <em>Automatically detect from the
                installation media/source</em>)</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="4ece2582-df17-4026-a3fe-feb30ae34a80"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-2.png"
        mediatype="img" alt="" width="400" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:400px;"></div>
<ol data-block-id="b5feb113-5076-4ab4-bcbc-797ce33cb19e" start="8">
    <li data-block-id="52981a94-0592-444c-9199-567b75732787">
        <p data-block-id="7018e987-3e6a-4537-926a-76154738be34">Select <strong>Memory</strong>=4096, and
            <strong>CPUs</strong>=2</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="3a6356f5-fea3-4f4c-8ac1-96ea63a707ad"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-3.png"
        mediatype="img" alt="" width="400" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:400px;"></div>
<ol data-block-id="e436f5c8-4e0d-4e52-a2db-65759b522553" start="9">
    <li data-block-id="3c167824-531f-47ec-a85f-510610d34dcc">
        <p data-block-id="7368a231-0eaf-4812-920d-8ef715bc6b1b"><strong>Create a disk image for the virtual
                machine</strong> of 25GiB or greater</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="4e720ffb-f1cf-41d9-a145-3b2e9a01156e"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-4.png"
        mediatype="img" alt="" width="400" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:400px;"></div>
<ol data-block-id="b1ff35e2-c4a7-4d74-997e-23ed337f6c14" start="10">
    <li data-block-id="99b30629-b0e3-4843-9cf0-52f06f8bfce3">
        <p data-block-id="f6a563ae-c24e-4ed3-8746-6ebd64a3e059">On the <strong>Ready to begin installation</strong>
            page: </p>
        <ul data-block-id="5a5338d5-4fc0-4c30-94b2-2ca0dc5f44f1">
            <li data-block-id="c04e9166-5e51-49e7-be3f-4abd9f391767">
                <p data-block-id="120fbdc9-89a4-4189-ba1c-450cfe6e386d">Enter <strong>Name</strong> for the VM, e.g.,
                    <em>vsr-kvm-1</em></p>
            </li>
            <li data-block-id="2f3bda6f-ab32-4b5b-b88e-43838e322a4f">
                <p data-block-id="f7ba626b-9a78-4cfe-9818-801110ab5ca4">Click <strong>Customize configuration before
                        install</strong></p>
            </li>
            <li data-block-id="d55470a8-aa64-4aae-8a70-ef05e24276da">
                <p data-block-id="ae5eca85-5e0c-46dc-8ceb-4cc1d116e998">Select <strong>Network selection &gt; Virtual
                        network 'default': NAT</strong></p>
            </li>
            <li data-block-id="c9fa7db0-3917-4d7b-9747-f9f8c8d2954b">
                <p data-block-id="941d4514-d39f-45ac-b568-f965e1cf70e6">Click <strong>Finish</strong></p>
            </li>
        </ul>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="feaf1d5b-8b4d-4f02-b43b-9ff4235ba1f4"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-5.png"
        mediatype="img" alt="" width="400" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:400px;"></div>
<p data-block-id="b6da9d85-c631-40b9-9799-379bbbfa1fbb">The following window displays:</p>
<div class="image-view center" data-type="media-content"><img data-block-id="e03b420d-791b-4b92-948f-e976f0c5bf03"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-6.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="e80c1643-199f-4896-bff3-af2d590051ee">The following configurations are required prior to <strong>Begin
        Installation</strong></p>
<ol data-block-id="925b5c02-0080-4a44-a129-4e216f6c2342">
    <li data-block-id="6e420716-cdc0-49a9-a213-3bc5f38e67d4">
        <p data-block-id="8a570fca-60f8-4ba2-8d6a-13d602c6b3b4">Select <strong>Overview &gt; Firmware &gt; UEFI
                X86_64:/usr/share/OVMF/OVMF_CODE_4M.fd</strong>. Apply the changes.</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="ffd4b428-35f2-4549-ac58-17ad23f70a1b"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-7.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="00e60d46-7185-4911-bd70-33ada14df9e1" start="2">
    <li data-block-id="df1a6d0a-2504-4a44-808d-ee230df7fcd9">
        <p data-block-id="d14c9031-daf3-4161-a0e7-9cadaec45975">Select <strong>Disk 1 &gt; Disk bus: SATA &gt;
                Apply</strong></p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="a75a1908-5fe8-4563-861a-d66bda480573"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-8.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="f65ff5a7-0ca8-4249-bba9-297be94e3966" start="3">
    <li data-block-id="946b2fa4-665d-4774-ba43-f2c578d1e3ef">
        <p data-block-id="2dde4174-cf62-447c-954e-b71344bf793b">Select <strong>Add Hardware &gt; TPM &gt; Type: Emulated
                &gt; Finish &gt; Apply</strong>.</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="40af6b2e-f82d-45ce-9a2e-afef28ddb327"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-9.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="fdff5967-35d3-47ba-bc7a-7f5de4fe184a" start="4">
    <li data-block-id="3ef78483-71f9-4d33-acd1-52cb28fd2c18">
        <p data-block-id="4c7f1943-e66b-425b-b7dc-087ab22edf7c">Select <strong>Add Hardware &gt; Serial &gt; Device
                Type: Output to a file (file)</strong></p>
        <ul data-block-id="f30addb0-a113-4a54-9adc-2ef7f4d122be">
            <li data-block-id="ad25aca5-0f18-4f47-858b-5830792af093">
                <p data-block-id="2bd4bc30-8fc7-4555-892d-bb5fa8dec730">In <strong>Path</strong> enter a file path,
                    e.g., <em>/tmp/vsr-kvm-1.serial</em></p>
            </li>
            <li data-block-id="1fb348bf-99fc-4c2f-9217-5ed3802c5231">
                <p data-block-id="8250d4be-2daa-4609-a1ec-acc89c8c1a6e">Select <strong>Finish &gt; Apply</strong></p>
            </li>
        </ul>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="e58a2fbb-cea2-46c3-bbbf-ea5746d1c153"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/kvm-vm-10.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="b6158d47-d5fe-4060-afee-7e701b6c9331" start="5">
    <li data-block-id="c25a0c8a-5f3d-4406-a3df-28173d01b06a">
        <p data-block-id="0774b3b8-41a2-4039-b9f5-b3c97b56aa6b">Click <strong>Begin Installation</strong>. The VM
            installation process starts.</p>
    </li>
</ol>
<p data-block-id="e8ef46c0-55a0-482c-a02b-db39615c8d08">The VM installation process is:</p>
<ol data-block-id="5e18728b-c8a0-4515-9fe7-5ec8513fdb12">
    <li data-block-id="0fe828a6-b742-404e-953d-9cb46ed70757">
        <p data-block-id="f0c982ef-f832-45ac-bca4-849da7847fe7">Select <strong>Normal Nodegrid installation</strong></p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="72494f90-ec7d-4c5c-9117-28d4725039d8"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-1.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="71dd726c-b5e5-44c1-996a-238d6cfcc69e" start="2">
    <li data-block-id="8377d721-0a2a-4c6a-87b8-9cd65a01cf32">
        <p data-block-id="f6b9995b-12b7-4ee3-a1d6-efedaa8038ee">To accept the License Agreement, enter <em>accept</em>
        </p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="d125ab94-7c3e-4f73-bd15-98118cad6be4"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-2.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="dbc3b7a1-d272-4626-ac55-9a3a179f1440" start="3">
    <li data-block-id="ca8d9210-8678-43e3-8839-5652c4cd5a81">
        <p data-block-id="364b74c5-4c3c-4fd4-bf89-8fec6912f4af">The Nodegrid Manager installation process shall take
            place. Once finished, reboot the VM</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="3359a4f4-5d77-496d-88d3-838008d239fd"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-3.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="e390ad1f-ad59-4a3f-8113-4604c76812c0" start="4">
    <li data-block-id="8b11c4c9-e62b-42a7-9ad9-23de39da37ca">
        <p data-block-id="3b4f03ce-059b-4e11-94a4-a771d382bf4c">After the VM reboots, access the Nodegrid Manager
            terminal with these credentials:</p>
        <ul data-block-id="babb61c6-4bbe-47fa-8fe0-b743f71282f2">
            <li data-block-id="81d8e7b2-7db1-4e1f-ac76-c5ef99664b49">
                <p data-block-id="9e913ed6-a9e6-4a55-a6e4-6a0a223f9ada">user: admin</p>
            </li>
            <li data-block-id="3ec58f55-8d30-4e9c-80ef-67770e712c86">
                <p data-block-id="3bb31ed3-59dc-4f24-ac7a-8169e778fed2">password: admin</p>
            </li>
        </ul>
    </li>
    <li data-block-id="d6cd8647-723e-461f-a2ff-05fbfda63022">
        <p data-block-id="c9f27c35-ae63-4b53-8572-7b3bde3ade96">Follow the process to change the admin password</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="a989aec5-70e7-4b90-9df3-bcc409ef23af"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-4.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="28c9eb65-99e3-441a-a644-9e78ffb8b978" start="6">
    <li data-block-id="55d630a6-7c13-4029-b344-fcb45a7bc460">
        <p data-block-id="ea8e178d-fd13-43df-a65a-6cea6d30cb4c">On the CLI, execute the following commands:</p>
    </li>
</ol>
<pre data-block-id="e6953dda-53b2-48b4-ae77-2cd4eb99c1c2" language="plaintext" class="language-plaintext"><code class="language-plaintext" spellcheck="false">show settings/network_connections/
show system/routing_table
</code></pre>
<div class="image-view center" data-type="media-content"><img data-block-id="d0f5b796-3ed6-45df-a9b7-a204a8d9910d"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-5.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="500e7d8b-09fd-499e-a388-a6708caf3aad">In this example, the IP address assigned to the Nodegrid Manager
    is <code>192.168.122.171</code>. The next section details how to access the Nodegrid Manager Web UI.</p>

## Web Access to the Nodegrid Manager
<p data-block-id="3552ffaa-6dbd-48fe-a5e9-4dec5bed5677">To access the Nodegrid Manager WebUI depends on the client
    location: 1) access from the KVM hypervisor (same host), 2) access from a remote client (KVM hypervisor in a remote
    server)</p>
<p data-block-id="96689e5d-2759-43c1-b7ce-c32015b6980c">For the first case:</p>
<ol data-block-id="59b0774e-1d59-4045-bec7-096f00faef7a">
    <li data-block-id="736c0f01-ac1a-4226-b411-8bf87bacd487">
        <p data-block-id="8ab6f5e5-1104-4060-8e51-bbff6ecda33f">Open the link https://private-IP in a browser, e.g.,
            https://192.168.122.171</p>
    </li>
    <li data-block-id="a2a80e23-6765-4b24-a97e-321e0e8e436c">
        <p data-block-id="55ceb38b-28da-47ee-a027-05890577fdd1">Log in to the Nodegrid Manager Web UI. Default
            credentials:</p>
    </li>
</ol>
<ul data-block-id="1d051739-1b2c-4496-8af9-4702c765ea01">
    <li data-block-id="c2e51d70-d8d5-496b-83f2-e7bb36362b18">
        <p data-block-id="1af5ebe5-8497-4f41-a1c2-14a584d15d2f">user: admin</p>
    </li>
    <li data-block-id="9dba59ab-1053-4ac3-bba5-53bed7e7326a">
        <p data-block-id="2f7f31f4-8e24-4107-ae55-a69d046c6051">password: admin</p>
    </li>
</ul>
<ol data-block-id="fb5e978b-4229-4fd0-a2d7-d6752f5b7674" start="3">
    <li data-block-id="8456b132-a2ce-48a4-ab1d-fc9107b08498">
        <p data-block-id="d58dda62-65de-44b2-8631-2be3e9581235">Change the password</p>
    </li>
    <li data-block-id="43465af0-3e35-4c94-ab77-2bc6ddecb256">
        <p data-block-id="cd32c630-4596-43c2-81ac-fbbe6d57d6f7">Congratulations! You have successfully deployed a
            Nodegrid Manager</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="35601305-a76b-49d8-8d47-ff86a20933c6"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/web-ui-local.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="a21a7cc9-98be-456c-9eba-7c8442fd9480">For the second case, the following options are:</p>
<ul data-block-id="2cb2e6f1-75ad-43c5-b405-13aa8a1dd4d5">
    <li data-block-id="fe656d79-f919-414b-bb4c-842af51400cb">
        <p data-block-id="585b56e1-d853-40e0-97e2-688df95523ee">Add a new interface to the VM that is bridged to your
            local LAN</p>
    </li>
    <li data-block-id="9e232ecf-d4c4-4680-9250-f7f344f229cd">
        <p data-block-id="a1da25c1-0cb3-4a05-b8f2-7bd334c4c44a">Forward TCP/80 and TCP/8080 ports on the hypervisor
            toward the VM</p>
    </li>
</ul>
<h2 data-block-id="5835f159-c9f6-4d46-9f51-8e56abcf3009">5. Enroll Nodegrid Manager to ZPE Cloud</h2>
<p data-block-id="59580282-299e-4974-ae1c-a6b6a60ea65e">A Nodegrid Manager can be managed from ZPE Cloud. It must be
    enrolled to the customer's ZPE Cloud instance.</p>
<ol data-block-id="deed2242-d585-4cfd-b69a-fd6674ac16fa">
    <li data-block-id="fa98e586-14cf-4905-98bf-9b3361c48a07">
        <p data-block-id="d3e064ca-49e3-4f12-9376-7345f8d2a375">Login to the ZPE Cloud account <a
                href="https://zpecloud.com" target="_blank">Global</a> , <a href="https://zpecloud.eu"
                target="_blank">EU</a>, or onPrem</p>
    </li>
    <li data-block-id="8103226e-0073-4a12-81d2-45f6829d10b2">
        <p data-block-id="ba3ee731-0457-4f48-888b-1b5f7f3c6f36">Go to <em>SETTINGS :: ENROLLMENT :: CLOUD</em>.</p>
    </li>
    <li data-block-id="4ec2576f-a28b-4b12-8afe-37e5633051f4">
        <p data-block-id="60c1a63f-1959-438a-b0ba-03cdf750af0f">Copy the <strong>Customer Code</strong> and
            <strong>Enrollment Key</strong> (required to claim the vSR).<br type="inline">&nbsp;<img
                data-block-id="9f97459b-426d-442b-97f9-364e21f347e2"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/settings-enrolment-cloud.png"
                alt="settings-enrolment-cloud" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="4d131eb2-7dd9-40eb-9cb4-7d70d5338584">
        <p data-block-id="2220cecd-10c8-46fd-91a8-23644ed6246b">In a browser, login to Nodegrid Manager with
            <strong>https://</strong>.</p>
    </li>
    <li data-block-id="a3c44fe2-b107-4301-87cf-57bf4d470344">
        <p data-block-id="dc5a49c7-799f-4baa-b075-60c251ceefd3">Go to <em>Security :: Services</em> and enable ZPE Cloud
            service<br type="inline">&nbsp;<img data-block-id="1fb05e68-a1a1-4c1f-abc6-c9c75db9f16f"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/security-zpecloud.png"
                alt="security-zpecloud" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="7c276245-bb21-4c8f-9243-e12646c6d7d6">
        <p data-block-id="17111219-2a56-4237-8048-a1535ba578ab">Go to <em>System :: Toolkit :: Cloud Enrollment</em>.<br
                type="inline">&nbsp;<img data-block-id="66296129-2d6f-469b-91cc-401d652a3928"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/system-toolkit.png"
                alt="system-toolkit" width="800" type="inline-block" fixaspectratio="false" mediatype="inline-block-img"
                autoaspectratio="false" shadow="no" border="no" round="no" heightauto="true" widthauto="false" style="">
        </p>
    </li>
    <li data-block-id="7cd06c3a-2950-422f-b731-de98b06f6ec4">
        <p data-block-id="522f9bc5-1e74-4579-8168-f3cc2d0cf4ed">Enter the following information </p>
        <ol data-block-id="4c152c10-d741-4940-ac68-21007a8cd4bd">
            <li data-block-id="bb34b2ec-d52d-427c-ae6e-8b1f2c6cc5a1">
                <p data-block-id="387baed3-77af-48cc-a748-73117cd7e083"><strong>URL</strong>: URL of the zpecloud
                    instance, default https://zpecloud.com for US users and https://zpecloud.eu for EU users.</p>
            </li>
            <li data-block-id="95c2c8cd-01f7-4fdb-9f96-c6d0cf2d27b6">
                <p data-block-id="e660eab7-34b3-44f7-8984-ab3b020e1b91"><strong>Customer Code</strong>: Use the copied
                    Customer Code from the Cloud Instance</p>
            </li>
            <li data-block-id="2c3c7f49-556f-43e7-b259-11aa237294ca">
                <p data-block-id="662df694-7cee-4ba1-9c98-78a7bae7895c"><strong>Enrollment Key</strong>: Use the copied
                    Enrollment Key<br type="inline">&nbsp;<img data-block-id="6bd2bac3-009b-4d05-a1ba-84013a399a0f"
                        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/settings-enrolment-cloud.png"
                        alt="settings-enrolment-cloud" width="800" type="inline-block" fixaspectratio="false"
                        mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                        heightauto="true" widthauto="false" style=""></p>
            </li>
        </ol>
    </li>
    <li data-block-id="2edcbbfa-9d06-4353-917c-e5950879213a">
        <p data-block-id="d2ebf9c5-7723-4e24-b41e-750f57af5e86">Click <strong>ENROLL</strong>.<br
                type="inline">&nbsp;<img data-block-id="47c5e53d-9418-4ece-aca2-470b89a28df0"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/system-toolkit-cloud-enrolment-success.png"
                alt="system-toolkit-cloud-enrolment-success" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="44622b76-37e1-4053-8a0b-591e0acb2a09">
        <p data-block-id="c0430595-dcc3-4faf-bd9b-b7289153a027">The unit is enrolled on ZPE Cloud and become available
            in ZPE Cloud under <em>DEVICES :: AVAILABLE</em>.<br type="inline">&nbsp;<img
                data-block-id="057da44e-bf91-4682-b43e-76128288bd68"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/devices-available.png"
                alt="devices-available" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="2dcfe5a7-b331-43e8-b1ef-b7b12a8713ed">
        <p data-block-id="643d90d7-716a-49fa-a8b3-54b13b40a497">To start management of the vSR, select and click on
            <strong>ENROLL</strong>.</p>
    </li>
    <li data-block-id="c77d2fcf-7590-4ba4-9699-0b5149d9bb55">
        <p data-block-id="6e3a9d7e-6512-4fef-a208-fdafc6547046">When enrolled, the vSR is managed on ZPE Cloud the same
            as any other Nodegrid device.</p>
    </li>
</ol>
<p data-block-id="d1f27036-031b-460e-b7ac-379758580a42"></p>