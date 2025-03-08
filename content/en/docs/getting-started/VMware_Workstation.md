---
title: Nodegrid Manager installation on VMware Workstation
date: 2017-01-05
weight: 3
description: >
  This documentation details steps to create a Nodegrid Manager VM instance on VMware Workstation
categories: [installation]
tags: [installation, vMware, docs]
---

## Requirements
<ul data-block-id="d2cc2ea3-0ad0-4d03-b8e6-131645c7af98">
    <li data-block-id="22bd5d18-5b53-457a-b94f-f2c5a0f65fb2">
        <p data-block-id="e55b754a-80a8-4d55-a7c9-5d08bfcf4c74">VMWorkstation 14 or later</p>
    </li>
    <li data-block-id="9519cae6-d8c5-415c-8270-0a5a77a630e2">
        <p data-block-id="e2b343a0-2f1a-4dbf-9496-19f8c0a2313c">Nodegrid OS image version 5.8.2 or higher (recommended)
        </p>
    </li>
</ul>

## Preparation

### Nodegrid Manager ISO image
<p data-block-id="018ad334-3901-4d0c-9da7-1fabbd2a7597">The following steps describe how to obtain a Nodegrid Manager
    ISO file:</p>
<ol data-block-id="4ab1cde5-4042-4ec9-87c7-1f33a772b31d">
    <li data-block-id="c9b5429f-09ef-4847-9570-a6e65453e95f">
        <p data-block-id="bbf2167d-2e2e-44a5-8111-8ffa18dda640">Access with your credentials to <a
                href="https://zpecloud.com" translate="no">https://zpecloud.com</a> or <a href="https://zpecloud.eu"
                translate="no">https://zpecloud.eu</a> depending upon the region.</p>
    </li>
    <li data-block-id="648fa362-f016-4b67-ba36-9a157407901d">
        <p data-block-id="78bd7eb4-ed06-47bb-94c4-822a763e17c3">Go to <strong>PROFILES :: SOFTWARE</strong>. </p>
    </li>
    <li data-block-id="6bbde331-bdc5-4ffa-9982-5dedfa54bf33">
        <p data-block-id="a543a490-1eba-4ba5-ab27-0c870b2efd28">Select a VSR Nodegrid version, e.g.,
            <em>Nodegrid_Platform_v5.8.2_20230114</em></p>
    </li>
    <li data-block-id="e39cb5fe-5c93-4fa4-b5fe-21244860665a">
        <p data-block-id="0c81e029-5a9b-4824-9dce-453163d3c7dd">Download the ISO file</p>
    </li>
</ol>
<blockquote data-block-id="0f0fc1db-3172-4ddf-97d7-3629de533502" style="overflow:auto;">
    <p data-block-id="ba5e20ba-6df6-4cd6-b6e9-266a355192e7"><strong>NOTE</strong>: The iso file can also be obtained
        through the support portal.</p>
</blockquote>

## Create a Nodegrid Manager instance

## Create a Nodegrid Manager VM
<ol data-block-id="4b2972ba-4177-4be1-a357-6ee5629f5824">
    <li data-block-id="d8f85b5c-78b8-495c-bc26-773b17a4ca58">
        <p data-block-id="19f0ee72-b3e1-4e37-9cfe-5b616d734254">Open the VMware Workstation application.</p>
    </li>
    <li data-block-id="9364eb88-0d55-495e-bac4-367f9d93ac31">
        <p data-block-id="0c48dba4-bbbb-49e6-89d7-67f158dc4bad">In the File drop-down menu, click <strong>New virtual
                machine</strong>. This starts the VM wizard.</p>
    </li>
    <li data-block-id="9bbf4827-89a8-45e2-be13-72d24babf266">
        <p data-block-id="fc7fd1e3-c4ee-4b22-9a43-3cf253323b00">On the dialog: Select <strong>Custom
                (advanced)</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="8a180aa6-3e8e-433c-933e-cc4a565d205d">
        <p data-block-id="1a7233fe-d2d5-44a9-ac52-4bb344a170c6">On <em>Hardware compatibility</em> page: Select
            <strong>Workstation 14.x (or later release)</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="9b9bede8-578f-4410-85f8-86bde8927e8e">
        <p data-block-id="401595fe-bd9f-4b90-80f7-d4d8d45b88e0">On the dialog: Select <strong>Install disc image file
                (iso)</strong>. Locate and select the Nodegrid image iso file. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="754ca4bf-49f9-4a81-ae05-3e8f10c632aa">
        <p data-block-id="0106aad7-642d-4a10-8ed6-85e625dced3f">On the dialog <em>Guest operating systems</em>, select
            <strong>Linux</strong>.</p>
    </li>
    <li data-block-id="df82b70f-9465-4866-a3db-4727203526e9">
        <p data-block-id="9886cf82-738c-4230-9829-50832574174b">On <strong>Version</strong>, select <strong>Other linux
                4.x kernel 64-bit</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="733ed0d9-b38b-4f19-a451-84ae2e1822f2">
        <p data-block-id="5a040faf-0735-4ba0-a55f-1e95d5a5b312">Enter <strong>Virtual machine name</strong>. Select the
            <em>Location</em>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="5d57f6d9-3037-4525-84b7-1f0b48487f3e">
        <p data-block-id="02a4f2e3-b6f6-4e8b-af67-3ba8335c7db6">For <strong>Number of Processes</strong>, enter
            <strong>2</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="410e9575-22cd-40eb-9784-3c8753b99bb0">
        <p data-block-id="19308c75-dee9-4732-a1e4-c4e60095d419">For <strong>Memory for this virtual machine</strong>,
            select <strong>4096Mb</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="a0d4cf27-2409-4dd6-9c3d-13e656a91aaf">
        <p data-block-id="49d3e370-d2b7-4ffa-b0c5-9b53211d034c">Select <strong>Use network address translation
                (NAT)</strong> checkbox. <strong>Click</strong> Next.</p>
    </li>
    <li data-block-id="6fc05267-8afe-4537-bc90-e42f3d774d34">
        <p data-block-id="a9ee4294-1216-4e96-98e6-ea933097448e">For <strong>I/O Controller Types</strong>, select
            <strong>LSI Logic</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="2866cdd6-3b6b-4ae4-ad9b-a92e5ed31d2c">
        <p data-block-id="67bd7c79-b441-4921-a8da-6f6f21aca11e">For <strong>Virtual Disk Type</strong>, select
            <strong>SCSI</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="d6416962-d409-4289-a58f-ead98a83c848">
        <p data-block-id="78232f3c-1424-444a-9e93-4e18718a23a1">Select <strong>Create a new virtual disk</strong>
            checkbox. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="e8b6c03e-4eea-4886-bde9-7dd80b7aeaab">
        <p data-block-id="4570207c-8306-4366-ad1f-92607d4ffe66">For <strong>Maximum Disk</strong> size, select
            <strong>32Gb</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="76c4a583-9782-4b47-bfa6-adf40c6425d1">
        <p data-block-id="57e7ad65-715b-4258-9dc9-8a7b897c2c9b">(no changes), click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="b9faffc3-b8fd-4558-9086-d069dd16ea1f">
        <p data-block-id="e9376d84-eb3c-4f09-8bbd-af6dafdef37c">Click <strong>Finish</strong>.</p>
    </li>
</ol>
<p data-block-id="ae775cf5-9119-436d-a7f8-3cdf8d6d9fc9">On <em>Library</em> view, locate the created VM. Select the VM.
    Right click and select <strong>Settings</strong>.</p>
<ol data-block-id="0a1bea40-4772-4327-b9f7-7dfb46e6e9d9">
    <li data-block-id="d3db62b3-b27b-4e1c-9195-f321360c3ca0">
        <p data-block-id="f39e1a05-832b-4ad9-9c57-29f386591a55">On <strong>Options</strong> tab, <em>Advanced menu</em>,
            for <strong>Firmware Type</strong>, select <strong>UEFI</strong>.</p>
    </li>
    <li data-block-id="1073e320-07df-486f-9de8-e199578a5e64">
        <p data-block-id="548c773b-065c-4f24-9210-b4a058476303">On <em>Access control</em> menu, click
            <strong>Encrypt</strong>.</p>
    </li>
    <li data-block-id="096054d1-59bf-4b7b-9886-10870baf8c3f">
        <p data-block-id="4e25df85-979b-4b48-b075-cef9cc848043">Enter a <strong>Password</strong>.</p>
    </li>
    <li data-block-id="6e717fce-bd43-4e71-9dc1-aab40fed7984">
        <p data-block-id="4c1bbed9-8f91-48af-8616-c0b214114630">Click <strong>Encrypt</strong>.</p>
    </li>
    <li data-block-id="6c50598d-2819-468d-99b6-1f160b2a9c90">
        <p data-block-id="200b4681-19f5-4bfb-9d58-d062eb027869">On <strong>Hardware</strong> tab: Click
            <strong>Add</strong>.</p>
    </li>
    <li data-block-id="2e6b7ed0-ec14-4b23-9ff0-8768602901ad">
        <p data-block-id="8c9b12cc-ba72-4497-8eaf-cb81a171dcca">Select <strong>Trusted Platform Module</strong>
            checkbox. Click <strong>Finish</strong>. Click <strong>OK</strong>.</p>
    </li>
    <li data-block-id="ffe95931-ec88-4f05-b523-5f842bbaa955">
        <p data-block-id="52e67424-e6cd-4310-9eb9-610e16135432">Start the VM.</p>
    </li>
</ol>

### Installation of Nodegrid Manager
<ol data-block-id="c7e40f52-3c9a-4b68-8baf-c86d89f74fde">
    <li data-block-id="8ccc3d02-18ec-46d8-bf8f-1ada9ad63b37">
        <p data-block-id="f3a9fa09-d58e-4ed8-bfaf-eca43813c84f">Select <strong>Begin Installation</strong>. The VM
            installation process starts.</p>
    </li>
    <li data-block-id="4438df9f-a8c5-4a8d-9862-3a9910e8194f">
        <p data-block-id="f15b4418-ff06-438a-b870-6a47130307b3">Select <strong>Normal Nodegrid installation</strong>.
        </p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="b4288f70-6df8-42f7-b508-69fc99e10e6a"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-1.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="d6433c5c-2f61-424b-b779-a220923dfc3d" start="3">
    <li data-block-id="9cbfcf28-c562-45e8-ab22-7280c798da52">
        <p data-block-id="c5aad1d3-34d9-4628-806a-12191fb8892c">To accept the License Agreement, enter <em>accept</em>.
        </p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="8e5aec4d-3364-4318-8653-f783ffb275c6"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-2.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="6414af55-ae78-48fc-a8b0-c70797cacef0" start="4">
    <li data-block-id="1686de2b-2ac7-4964-b8d3-96c7ceafc88d">
        <p data-block-id="a631f992-2276-4894-b2a0-937c6913b72b">The Nodegrid Manager installation process begins. When
            finished, reboot the VM</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="b7a558d5-6ef7-4ca9-b2ce-355e1e74ebed"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-3.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="fe3d6e9f-6803-494e-9623-232696cebae1" start="5">
    <li data-block-id="8d77fa07-50e2-4d7a-a873-0caff6206657">
        <p data-block-id="d90ef114-5318-40dd-bce6-a34de32ee9df">After the VM reboots, access the Nodegrid Manager
            terminal with the following credentials:</p>
        <ul data-block-id="0b6020db-50a1-4164-92ea-b69c0264d3ed">
            <li data-block-id="aebd427c-922e-466c-bebb-35056bb098a2">
                <p data-block-id="d99f6f00-2b72-4700-bedf-a4c80331b754">user: admin</p>
            </li>
            <li data-block-id="a954098a-f60b-4b5b-b585-9c59cd3b8e31">
                <p data-block-id="b4bbc004-5482-4765-a407-48115b55f49e">password: admin</p>
            </li>
        </ul>
    </li>
    <li data-block-id="e4e9cd57-f9bf-4080-9dfd-9e3a264708a9">
        <p data-block-id="24ac23bc-1429-469c-9951-73b180ea4aad">Follow the process to change the admin password</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="52a1c5e2-6409-4b50-a5c4-b527140a00bf"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-4.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="41caba91-c8c8-432a-92dd-b5425610149b" start="7">
    <li data-block-id="bd548466-5f4a-4d03-8cb2-822b7fff3256">
        <p data-block-id="b908cfc3-2908-4440-afeb-4b5adba44a28">On the CLI, execute:</p>
    </li>
</ol>
<pre data-block-id="2dc9ebec-1d38-4629-8757-56cee2bafb93" language="plaintext" class="language-plaintext"><code class="language-plaintext" spellcheck="false">show settings/network_connections/
show system/routing_table
</code></pre>
<div class="image-view center" data-type="media-content"><img data-block-id="4f122e95-9e54-4dfe-8fc7-94258fd8a963"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-5.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="73e00ef9-550e-474d-b705-9548ad87810f">In this example, the IP address assigned to the Nodegrid Manager
    is <code>192.168.122.171</code>.</p>

## Web Access to the Nodegrid Manager
<ol data-block-id="435be42c-6b45-4024-a5a3-056fa11e395a">
    <li data-block-id="5ec2d728-81e9-44e9-a1ad-d104d06ecd1f">
        <p data-block-id="e33d1366-91e9-4ff5-a9bb-f7051892453c">Open the link <strong>https://private-IP</strong> in a
            browser, e.g., https://192.168.122.171</p>
    </li>
    <li data-block-id="44b9b54e-b258-47b2-b6e5-076b83e8713b">
        <p data-block-id="c9369fbd-f877-4246-a065-4f0cfd253b07">Log in to the Nodegrid Manager WebUI. Default
            credentials: </p>
        <ul data-block-id="abce025e-3acb-49bf-ab6f-65769ed41d82">
            <li data-block-id="4ef0e20d-5dac-4d13-b4ba-cc1cb7e593a9">
                <p data-block-id="100e2a57-1969-46e3-965d-25bae282488c">user: admin</p>
            </li>
            <li data-block-id="5791fb13-f4fd-4043-9e2c-150bb885d6d7">
                <p data-block-id="25eceb96-fa79-45b2-9129-bfdb2bb2c7fb">password: admin</p>
            </li>
        </ul>
    </li>
    <li data-block-id="b8bd369d-943c-41f0-9164-290d24b43f5d">
        <p data-block-id="a6b8fa4f-50b2-4ef9-98ca-92b022ce5bab">Follow the steps to change the password.</p>
    </li>
    <li data-block-id="7883ed10-21ea-4876-9943-ed8b7a15ca84">
        <p data-block-id="556de076-18ce-4fdc-95f0-584c58ef2df9"><strong>Congratulations!</strong> You have successfully
            deployed a Nodegrid Manager.</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="f742d556-d891-4bca-93ed-01092156a619"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/web-ui-local.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="5c7c5ead-b3b7-40db-a400-d6573c55e810"></p>