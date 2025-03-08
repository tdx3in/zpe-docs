---
title: Nodegrid Manager installation on VMware vSphere
date: 2017-01-05
weight: 2
description: >
  This documentation details steps to create a Nodegrid Manager VM instance on VMware vSphere
categories: [installation]
tags: [installation, vMware, docs]
---

## Requirements
<ul data-block-id="6fc18247-90d6-4d58-bf58-d024defd2d5a">
    <li data-block-id="ab8b5fb4-3d96-44f2-a34c-2ad040603bcc">
        <p data-block-id="48d145b6-0d24-47c8-ae07-220985f91129">EFI firmware</p>
    </li>
    <li data-block-id="c5e76c97-6c6d-4468-9829-0b4a40b9714e">
        <p data-block-id="2cd45f29-d7d7-4971-821a-382fb37737cd">On vCenter 7.0 U2 and later this component is available
            by default</p>
    </li>
    <li data-block-id="0f7294da-0ffc-4e73-a496-d962327fd27f">
        <p data-block-id="2d3ad791-02b8-445a-8484-57296d4859cd">Datacenter in Cluster</p>
    </li>
    <li data-block-id="5a9a1028-f99d-45be-8284-20c5d8a80c08">
        <p data-block-id="73b76076-90eb-4e7d-9562-4a4e0432f213">FQDN (datacenter hostname) different from default</p>
    </li>
    <li data-block-id="69538869-2497-4026-aa8e-3a028e2ff16e">
        <p data-block-id="06052e47-389a-4042-a522-d369fa2052a8">Nodegrid OS image version 5.8.2 or higher (recomended)
        </p>
    </li>
</ul>

## Preparation

### VMware: Configure a Native Key Provider
<p data-block-id="35f84cd3-8df2-4d53-8fe8-4b6bd600894b">Nodegrid Manager requires access to vTPM to be fully functional.
    vTPM functionalty is provided through a Native Key Provider. This section outline the configuration of a Native Key
    Provider for Nodegrid Manager</p>
<blockquote data-block-id="9a56dd21-8d77-4d9e-a464-26534e85462e" style="overflow:auto;">
    <p data-block-id="cbe6d7b9-d25b-46c3-960c-c83a7be27726">For more information about VMware Native Key Provider, see
        <a href="https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-54B9FBA2-FDB1-400B-A6AE-81BF3AC9DF97.html"
            target="_blank">vSphere Native Key Provider Overview (vmware.com)</a></p>
</blockquote>
<p data-block-id="5dc371b3-c47c-40f9-b9ac-2f1cc512f24e"><strong>Required privilege:</strong> Cryptographic operations to
    manage key servers.</p>
<ol data-block-id="4c10a337-07f2-4c48-a5bb-82f15ee9ece5">
    <li data-block-id="2ac38149-7ed9-4685-b37e-b42281d740d3">
        <p data-block-id="d84cb70d-4fb4-4f2e-8ddc-b75933250651">Open the **vSphere Client **application.</p>
    </li>
    <li data-block-id="8ea188ad-74e3-4a51-bba1-736570a0cd6c">
        <p data-block-id="2ec19b6f-c818-4c58-8ab4-429adbe3a561">Log in to the vCenter Server system.</p>
    </li>
    <li data-block-id="be139eb0-20e1-4b31-92ac-3749cd7cb996">
        <p data-block-id="6e0bfce7-bd2e-47bc-ba42-b1be1ddc4219">Browse the inventory list and select the <strong>vCenter
                Server</strong> instance.</p>
    </li>
    <li data-block-id="b166a6e0-e78c-4948-bfa6-6ab7df7bc66d">
        <p data-block-id="ddeabb54-8277-4b5f-80d2-6cfa82f72c70">Click <strong>Configure</strong>,</p>
    </li>
    <li data-block-id="778ed54f-928a-452f-96e5-5c57f5a5236e">
        <p data-block-id="bb12055e-197a-4bc8-bf5f-262eb1f6d344">Under <em>Security</em>, click <strong>Key
                Providers</strong>.</p>
    </li>
    <li data-block-id="ac57beef-3b9c-4661-9d04-6d9c1bd910a7">
        <p data-block-id="68dfb615-728e-4cec-bcd2-782b730b9831">Click <strong>Add</strong>.</p>
    </li>
    <li data-block-id="465e4f6c-f1ed-42f2-bf2a-d651204e1302">
        <p data-block-id="345d5e01-92f0-4aa7-883d-9e308709fbbf">Click <strong>Add Native Key Provider</strong>.</p>
    </li>
    <li data-block-id="f04da9e0-6896-4943-8d39-90d4f04533bd">
        <p data-block-id="f2c72b29-d760-4351-b124-d5d7c533bf20">Enter a <strong>Name</strong>. Each logical key
            provider, regardless of type, must have a unique name. For more information, see <a
                href="https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-E5E8A9BF-F736-48D9-9DD4-A37F6333C692.html#GUID-E5E8A9BF-F736-48D9-9DD4-A37F6333C692__SECTION_9EFF1C43-DFE3-4DEB-978F-5A1F9BE3AE4A"
                target="_blank">Key Provider Naming</a>.</p>
    </li>
    <li data-block-id="e7d7f394-57aa-40e8-8c4d-6f93e0bccfe0">
        <p data-block-id="6696958d-182e-4bca-bd00-704659ac7a23">To utilize this vSphere Native Key Provider only by
            hosts with TPM 2.0, select Use key provider only with TPM protected ESXi hosts checkbox.</p>
    </li>
    <li data-block-id="9ce30eb6-a5f4-4c35-8376-d62fafcf9993">
        <p data-block-id="b7f799f0-1809-4ce9-9513-18088696343e">Click <strong>Add Key Provider</strong>.</p>
    </li>
</ol>
<section class="infoBox" style="background:#ddf7ff;" data-background="#ddf7ff">
    <div class="title">
        <p data-block-id="a63fc352-306f-4e55-b699-9b30e62a3a26">NOTE </p>
    </div>
    <div class="content">
        <p data-block-id="c52575af-ef73-4c10-a403-bb5e0a227bb2">Requires approximately five minutes for all the
            clustered ESXi hosts in a data center to get the key provider, and for the vCenter Server to update its
            cache. Because of the way the information is propagated, a few minutes may be needed before using the key
            provider for key operations on some of hosts.</p>
    </div>
</section>
<p data-block-id="0cd02f8e-43f1-4bd5-b503-c5b01d71aeae">The vSphere Native Key Provider is added and appears in the Key
    Provider pane. At this point, the vSphere Native Key Provider is not backed up. Before use, back up the vSphere
    Native Key Provider. See <a
        href="https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-E0EB371A-F6E4-463B-A1E9-9D4DDCAA039D.html"
        target="_blank">Back up a vSphere Native Key Provider (vmware.com)</a></p>
<p data-block-id="92c64384-560b-449d-a8e5-cf5e0269d469">To add vTPMs to the ESXi hosts, see <a
        href="https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-A43B6914-E5F9-4CB1-9277-448AC9C467FB.html#GUID-A43B6914-E5F9-4CB1-9277-448AC9C467FB"
        target="_blank">Securing Virtual Machines with Virtual Trusted Platform Module.</a></p>
<p data-block-id="c7ec1b81-f680-48dc-a1eb-020ef5939bbd">To encrypt virtual machines, see <a
        href="https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-A29066CD-8EF8-4A4E-9FC9-8628E05FC859.html#GUID-A29066CD-8EF8-4A4E-9FC9-8628E05FC859"
        target="_blank">Use Encryption in Your vSphere Environment.</a></p>


## Nodegrid Manager ISO image
<p data-block-id="1aeaed9d-9f9b-4bec-b82b-e8b07de1bdb3">The following steps describe how to obtain a Nodegrid Manager
    ISO file:</p>
<ol data-block-id="be9f6882-ab4e-4697-9ac1-2bc2c3bc083b">
    <li data-block-id="d7470d6b-143e-4cd4-bb9b-cea1179b586c">
        <p data-block-id="ef902661-f84b-44ae-aeff-dbd161c069d1">Access with your credentials <a
                href="https://zpecloud.com" translate="no">https://zpecloud.com</a> or<a href=" https://zpecloud.eu"
                target="_self" translate="no"> </a><a href="https://zpecloud.eu" translate="no">https://zpecloud.eu</a>
            depending upon your region.</p>
    </li>
    <li data-block-id="4e428dcf-2c91-4fb7-803b-cd4b6407459f">
        <p data-block-id="5a642047-2c8f-4096-85f8-a935e9c36c62">Select <strong>Profiles &gt; Software</strong></p>
    </li>
    <li data-block-id="9ce7e29d-9b4d-4cef-b6d6-9b0cc80e5eee">
        <p data-block-id="1fbc0e03-3289-442e-b7e5-f48af853aec7">Select a VSR Nodegrid version, e.g.,
            <em>Nodegrid_Platform_v5.8.2_20230114.</em></p>
    </li>
    <li data-block-id="a260aa97-5f9b-487d-9cf1-2e7f431f3743">
        <p data-block-id="69a13858-5dc4-4f94-9419-b44da5362e1f">Download the ISO file.</p>
    </li>
</ol>
<blockquote data-block-id="2d06582a-f3ef-4963-bf71-e0b1dfe45c07" style="overflow:auto;">
    <p data-block-id="65489a9a-5290-488d-bace-f1812ce11fb0">NOTE: The iso file can also be obtained through the support
        portal.</p>
</blockquote>
<h2 data-block-id="90916033-622f-42fe-bc7a-a0021b6b4f43">Create a Nodegrid Manager instance</h2>
<h3 data-block-id="ee2d1c09-2a4b-41da-acb5-10d371977461">Upload Nodegrid Manager ISO to Data Storage</h3>
<ol data-block-id="0440131d-c791-4371-ba02-44c246d2152a">
    <li data-block-id="14f82ae9-b80e-4934-9a34-7fb2df97a7ca">
        <p data-block-id="a4293293-fadf-48d2-90af-46da1945ae84">Open the vSphere Client application.</p>
    </li>
    <li data-block-id="3a5d3d21-46d8-4f44-b92a-683b7a5167a1">
        <p data-block-id="fea9d8a8-e5c5-429c-b662-66c8c216ae6e">Upload NG iso image to vCenter storage.</p>
    </li>
</ol>

### Create a Nodegrid Manager VM
<ol data-block-id="7ac3fd60-a719-45c9-be35-052b756fe79b">
    <li data-block-id="9e19a404-f2ce-4923-8823-be9f3bdbf2e3">
        <p data-block-id="511cb669-a18f-4bc5-8b20-0ad1d7a237bc">On <strong>Menu</strong> drop-down., select
            <strong>Hosts and Clusters</strong>.</p>
    </li>
    <li data-block-id="83a77c19-5525-4364-b6e8-f03cd2a82964">
        <p data-block-id="145f49f4-7a28-4e66-ac94-af33085de12c">On the <strong>Actions</strong> drop-down., select
            <strong>New Virtual Machine</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="3f2f4210-5803-4b21-ae65-671d31e61982">
        <p data-block-id="59e0a369-f0fb-4df0-bb9f-791c90b733a0">On the <em>Select a creation type</em> page: Select
            <strong>Create a new virtual machine</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="8b171d0a-12f7-4d6d-a1a3-810dd0dd10e0">
        <p data-block-id="4bae365f-811a-4086-9e24-e59e27fd410b">On the <em>Select a name and folde</em>r page: Enter a
            <strong>Name</strong> for the VM. Select the <strong>Location</strong> for the new VM. Click
            <strong>Next</strong>.</p>
    </li>
    <li data-block-id="d62f75d2-6117-4330-9e2c-d90a46f54657">
        <p data-block-id="a8b5dd31-71c3-4ea9-a3d0-e1c1995ce652">On the <em>Select a compute resource</em> page: Select
            the <strong>Destination Compute Resource</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="89cd4ad4-155e-4ec7-8c10-70af42caa006">
        <p data-block-id="bfb75a81-f6f8-492c-b731-af46edb40add">On the <em>Select storage</em> page: Select the
            <strong>Storage Configuration</strong>. Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="c9796279-6e50-4198-a8c4-a4a92b0b172e">
        <p data-block-id="2e4b2789-3213-4344-97cc-32575b04a9d7">On the <em>Select compatibility</em> page: On the
            <strong>Compatible</strong> drop-down., select <strong>ESXi 6.7 and later</strong>. Click
            <strong>Next</strong>.</p>
    </li>
    <li data-block-id="08baf66d-5853-41a3-bf88-06c9c3c25983">
        <p data-block-id="2ab938bb-4b38-4875-8ed3-395076139cc0">On the <em>Select a guest OS</em> page: </p>
        <ul data-block-id="266ddb6a-3d99-4f58-8115-5f0c5d07eb67">
            <li data-block-id="27fa1bab-3d2f-4d04-8cc0-5e94ca4152fb">
                <p data-block-id="2f75b4e8-9b37-40b4-9c8a-264641698cca">On the <strong>Guest OS Family</strong>
                    drop-down, select <strong><em>Linux</em></strong>.</p>
            </li>
            <li data-block-id="18e4ad33-ec78-442e-86de-970b7c1af9ea">
                <p data-block-id="5694105d-4e18-4ad5-9583-06be087fbecc">On the <strong>Guest OS Version</strong>
                    drop-down, select <strong><em>Other 4.x or later Linux (64-bit)</em></strong>.</p>
            </li>
            <li data-block-id="2c7cf3f2-7faf-4066-869e-5cd01ea85a56">
                <p data-block-id="ed7626d5-f882-4498-9970-c768e5a24dc7">Click <strong>Next</strong>.</p>
            </li>
        </ul>
    </li>
    <li data-block-id="b240f601-cddf-429f-bd2f-44b956dfc9de">
        <p data-block-id="8b972c78-453b-46f3-beee-ecd7df62aad0">On the <em>Customize hardware</em> page, <strong>Virtual
                Hardware</strong> tab, select:</p>
    </li>
</ol>
<div data-type="table-content">
    <table width="100%" class="editor360-table" borderstyle="Solid">
        <colgroup style="display:none;">
            <col style="width:25px;">
            <col style="width:25px;">
        </colgroup>
        <tbody>
            <tr>
                <th colspan="1" data-vertical-align="middle" data-horizontal-align="left" rowspan="1"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="e24c6ce2-b1f9-4d95-b19e-ffe99e3c9b8f">Setting</p>
                </th>
                <th colspan="1" data-vertical-align="middle" data-horizontal-align="left" rowspan="1"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="d4639ac3-1627-4c90-b7e3-6a58abf61309">Value</p>
                </th>
            </tr>
            <tr>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="ed9f7501-412a-42e9-ad83-613496a4c4ce">CPU</p>
                </td>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="06bc02cb-08ea-4f55-a87e-8ff1e2082aaf">2</p>
                </td>
            </tr>
            <tr>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="a969e295-e9e4-40eb-bb54-142f71c22c97">Memory</p>
                </td>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="596774c0-e117-4cd5-ad16-f1cb4bdba455">4GB</p>
                </td>
            </tr>
            <tr>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="a98467bd-6d4b-46a1-ad00-d87d8b6cca94">Hard disk</p>
                </td>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="0833e8bc-0633-434c-a76a-145455dde637">32 GB</p>
                </td>
            </tr>
            <tr>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="47b7eb8d-3581-46d6-955d-4433600f9711">Virtual device node</p>
                </td>
                <td colspan="1" rowspan="1" data-vertical-align="middle" data-horizontal-align="left"
                    style="vertical-align:middle;text-align:left;">
                    <p data-block-id="be3fcd28-51d5-4dca-8f6d-0fa6d863defa">IDE 0</p>
                </td>
            </tr>
        </tbody>
    </table>
</div>
<ol data-block-id="fe601904-506c-471c-9727-e8b03df7c920" start="10">
    <li data-block-id="f8f34774-b0ec-4ab9-a1dd-3f0332a0e60a">
        <p data-block-id="d526b4b9-cf6b-4a36-a874-df2e441e92aa">On New CD/DVD Drive - Datastore ISO File: Select the
            uploaded iso image. Select <strong>Connected at power on</strong> checkbox.</p>
    </li>
    <li data-block-id="f0d98cf0-b674-4d10-abb8-d533ffb1143f">
        <p data-block-id="6a631f8c-5b69-4ae5-acb0-dbfb3cabc682">To create a second network adapter, on <em>Add new
                device</em>, select <strong>Network Adapter</strong>. Under <em>New network</em>, for both network
            adapters, enter <strong>Adapter type = E1000E</strong>.</p>
    </li>
    <li data-block-id="1d00a7f6-d2a3-4106-a143-0eb727558fba">
        <p data-block-id="d72b3c38-dd2d-48ee-b71b-21f745cf2066">On the <em>Customize hardware</em> page, <strong>VM
                Options</strong> tab: Click <strong>Add new device</strong> and select <strong>Trusted Platform
                Module</strong>.</p>
    </li>
    <li data-block-id="6c22f175-78f2-4a12-8841-9c33f7828a66">
        <p data-block-id="bba5cbc3-8187-49d9-8fc7-68d645e5737d">On the <em>Customize hardware</em> page, <strong>VM
                Options</strong> tab: Under <em>Boot options</em> select:<br type="inline"> Firmware = EFI<br
                type="inline"> Secure boot = disabled**<br type="inline"> Click <strong>Next</strong>.</p>
    </li>
    <li data-block-id="e9852ba4-925f-4569-b349-acd661106139">
        <p data-block-id="cea56884-9526-4494-a152-585dd458a19f">On <em>Ready to complete</em> page: Review the VM
            configuration details. Click <strong>Finish</strong>.</p>
    </li>
</ol>

### Installation of Nodegrid Manager
<ol data-block-id="8c912427-9943-4ef7-bfcd-5c5548e3ab30">
    <li data-block-id="3737df27-0185-4b2a-9147-d022ced4b101">
        <p data-block-id="0031ec14-3295-475f-81ff-832cde917a57">Select <strong>Begin Installation</strong>. The VM
            installation process begins.</p>
    </li>
    <li data-block-id="ba8da129-93cf-4dd3-90a7-24ec3f6472ef">
        <p data-block-id="478cb482-7fd9-451f-a42a-f731a0e1b9f8">Select <strong>Normal Nodegrid installation</strong>.
        </p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="484b2456-f804-437d-98db-346f9fd5ba2e"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-1.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="7a5f3021-4117-4c18-9945-237439941e46" start="3">
    <li data-block-id="f122722e-3874-4d0c-9ecb-e6db3501f549">
        <p data-block-id="bfbecb62-65a1-4778-b243-44fbdb81756e">To accept the License Agreement, ether
            <strong>accept</strong>.</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="2d09c76e-3bd5-4819-b4af-7472bd1ed5d4"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-2.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="d59287b1-7448-4ba8-93bc-bba1e091d855" start="4">
    <li data-block-id="a3fdc793-2535-4ab0-bd65-9459403edc35">
        <p data-block-id="3bcec36d-8bc7-44f7-bab6-41058b034580">The Nodegrid Manager installation process begins. When
            finished, reboot the VM.</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="143909ba-03ae-49b3-b7ed-cc83113bc025"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-3.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="ceb5df7b-606c-4090-813a-c59833efd535" start="5">
    <li data-block-id="39276b23-0146-4229-bc4a-52791e41d7f2">
        <p data-block-id="57422b6e-8a05-4e78-b4d5-1ef9c90d8b62">After the VM reboots, access the Nodegrid Manager
            terminal with the following credentials:</p>
        <ul data-block-id="be1633a1-5016-4d8e-84bd-baf6df5ff274">
            <li data-block-id="3d14ae34-e281-4dc9-a45d-fb1af476f93b">
                <p data-block-id="4b877d44-0d9e-4e83-a276-cbeb50d585aa">user: admin</p>
            </li>
            <li data-block-id="6ad00a99-8fec-441f-8bf1-847c1d4c8521">
                <p data-block-id="e9490be6-a74f-44c2-92a9-c22886cb7d74">password: admin</p>
            </li>
        </ul>
    </li>
    <li data-block-id="f5a9a08e-fe2b-4921-b8a0-8eaea27e5ab0">
        <p data-block-id="cd85637f-44f3-4611-8e19-95d7b8a8257a">Follow the process to change the admin password</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="27619429-4bf9-4ef3-9dba-53964b03eb04"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-4.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<ol data-block-id="00f8d51e-ff24-491d-8080-41faa318c8ac" start="7">
    <li data-block-id="20bf8bcf-129c-4977-b806-b673744110ad">
        <p data-block-id="af91dbd6-a6c4-4c92-942b-d679ed541886">Execute the following commands on the cli:</p>
    </li>
</ol>
<pre data-block-id="5fe55b3c-1035-48ea-b8d9-34d0ecb094cb" language="plaintext" class="language-plaintext"><code class="language-plaintext" spellcheck="false">show settings/network_connections/
show system/routing_table
</code></pre>
<div class="image-view center" data-type="media-content"><img data-block-id="2d564ebd-85c8-4bba-8e63-cf45985ff4d1"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/vm-5.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>
<p data-block-id="48a12e9e-ce33-4071-b908-347c199678be">The IP address assigned to the Nodegrid Manager in this example
    is <code>192.168.122.171</code>.</p>

## Web Access to the Nodegrid Manager
<p data-block-id="2fa7a4fa-1052-4018-9c44-a55dff3c44ee">To access the Nodegrid Manager WebUI.</p>
<ol data-block-id="8f53a63c-b60f-4c97-a181-779e95075274">
    <li data-block-id="230cff35-d045-404b-88e1-88f9d3bd80cb">
        <p data-block-id="0e9eb625-7c3e-4e90-be93-73d23d2a70d0">Open the link <strong>https://private-IP</strong> in a
            browser, e.g., https://192.168.122.171</p>
    </li>
    <li data-block-id="60117c83-810c-4446-9219-17d0ada2c589">
        <p data-block-id="1547cc29-03b5-4a5e-a4c4-1d8c5773ce39">Log in to the with default credentials:</p>
    </li>
</ol>
<ul data-block-id="6125487e-c618-4e8a-a122-ee9f4fa14fda">
    <li data-block-id="976a5f68-0a5f-4904-bbc0-b79ecdcac9d0">
        <p data-block-id="7a2f9d90-9a62-4f90-9db1-e171aa1da8e6">user: admin</p>
    </li>
    <li data-block-id="26663aca-2bc1-453a-9408-4a13a94ecf6f">
        <p data-block-id="8d894389-a707-4bef-a0dc-463bde90df0a">password: admin</p>
    </li>
</ul>
<ol data-block-id="6e0b6d36-044a-4110-9ac8-ad1919465c84" start="3">
    <li data-block-id="3e2a5c64-3e3f-490c-8be5-de626c790358">
        <p data-block-id="35db7754-025c-4b11-8162-4816bc6dd26b">Follow the steps to change the password</p>
    </li>
    <li data-block-id="29da40ec-3949-480c-8b7e-f6e7deed689f">
        <p data-block-id="a94c1d3f-5a42-491c-b8a4-1869ad68a8d2"><strong>Congratulations!</strong> You have successfully
            deployed a Nodegrid Manager</p>
    </li>
</ol>
<div class="image-view center" data-type="media-content"><img data-block-id="8b6197ac-9d04-45ff-b6e4-354f19402ec7"
        src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/web-ui-local.png"
        mediatype="img" alt="" width="800" dataalign="center" datadisplay="flex" fixaspectratio="false"
        data-type="media-content" autoaspectratio="false" shadow="no" border="no" round="no" heightauto="false"
        widthauto="false" style="width:800px;"></div>

## Enroll Nodegrid Manager to ZPE Cloud
<p data-block-id="0094731e-d497-4ced-aba6-de649d6754a6">A Nodegrid Manager can be managed from ZPE Cloud. For this is it
    must be enrolled to the customer's ZPE Cloud instance.</p>
<ol data-block-id="6271374b-521a-4945-88ae-c373fdc48846">
    <li data-block-id="8caa7439-4a3e-475f-8e5c-c22d8d8ec755">
        <p data-block-id="c8d7db6a-66ad-467c-ac60-d98cec6a5e72">Login to the ZPE Cloud account <a
                href="https://zpecloud.com" target="_blank">Global</a> , <a href="https://zpecloud.eu"
                target="_blank">EU</a> or onPrem</p>
    </li>
    <li data-block-id="66a169eb-3244-450a-968a-f34df0ef4697">
        <p data-block-id="2d00311f-ded5-41d8-899d-2a6808d2106f">Go to <em>SETTINGS :: ENROLLMENT :: CLOUD</em>.</p>
    </li>
    <li data-block-id="9db92cd9-c995-43c4-a623-3461114b4e4c">
        <p data-block-id="cbd44187-533a-4fdc-adc8-113873d265ad">Copy the <strong>Customer Code</strong> and
            <strong>Enrollment Key</strong> (required to claim the vSR).<br type="inline">&nbsp;<img
                data-block-id="970b6f1e-bc46-4feb-b7cd-e928509e92e3"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/settings-enrolment-cloud.png"
                alt="settings-enrolment-cloud" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="67e3218b-d10f-4128-8e6f-d808bb3a9998">
        <p data-block-id="36beac5d-8db1-4b39-b3e4-a7419e9dafa1">In a browser, login to Nodegrid Manager with
            <strong>https://IP-ADDRESS</strong>.</p>
    </li>
    <li data-block-id="b4323970-4694-40d7-a1a4-fac8c4ae9ea6">
        <p data-block-id="b3a5796b-f474-4dec-b45d-9c764ae59b27">Go to <em>Security :: Services</em> and enable ZPE Cloud
            service.<br type="inline">&nbsp;<img data-block-id="aeddfacf-14de-4fa5-aacd-5b3d7d471a21"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/security-zpecloud.png"
                alt="security-zpecloud" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="abfd9ef3-1f22-42fa-a649-24bfa2f0b7ed">
        <p data-block-id="69640834-d645-4277-bc54-a823257c6b9b">Go to <em>System :: Toolkit :: Cloud Enrollment</em>.<br
                type="inline">&nbsp;<img data-block-id="025632fa-edad-4c61-ac83-f5084b67eca4"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/system-toolkit.png"
                alt="system-toolkit" width="800" type="inline-block" fixaspectratio="false" mediatype="inline-block-img"
                autoaspectratio="false" shadow="no" border="no" round="no" heightauto="true" widthauto="false" style="">
        </p>
    </li>
    <li data-block-id="998cd8a1-a2eb-4850-bd18-d523fa7a0261">
        <p data-block-id="28bd0853-65e1-440f-a43f-73e77ac6a2b4">Enter the following:<br type="inline"> a.
            <strong>URL</strong>: URL of the zpecloud instance, default https://zpecloud.com<br type="inline"> b.
            <strong>Customer Code</strong>: Enter the copied Customer Code from the Cloud Instance.<br type="inline"> c.
            <strong>Enrollment Key</strong>: Enter the copied Enrollment Key.<br type="inline">&nbsp;<img
                data-block-id="470cba9d-aa21-408b-bbff-c2a273c154b2"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/settings-enrolment-cloud.png"
                alt="settings-enrolment-cloud" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="542c52b3-2e7b-416b-a61d-9f0dad6ee671">
        <p data-block-id="02913eb8-dec5-4553-bc4b-9304c9c775b7">Click <strong>ENROLL</strong>.<br
                type="inline">&nbsp;<img data-block-id="7a14d019-dfdb-464e-bc5f-8dc1fb722cd8"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/system-toolkit-cloud-enrolment-success.png"
                alt="system-toolkit-cloud-enrolment-success" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="674cd0e5-cbba-4913-a9ec-b5d4f833bb52">
        <p data-block-id="6f4ad2d3-2086-40d8-b594-7c01dff2a07c">The unit is enrolled on ZPE Cloud and is available in
            ZPE Cloud under <em>DEVICES :: AVAILABLE</em>.<br type="inline">&nbsp;<img
                data-block-id="f4b1e2ea-1de1-4aa2-83d2-2a97891df51a"
                src="https://cdn.document360.io/763c5fb1-b9af-4ccd-9ad6-cf28ae4cd5a3/Images/Documentation/devices-available.png"
                alt="devices-available" width="800" type="inline-block" fixaspectratio="false"
                mediatype="inline-block-img" autoaspectratio="false" shadow="no" border="no" round="no"
                heightauto="true" widthauto="false" style=""></p>
    </li>
    <li data-block-id="5c3deaec-2851-4545-a000-4f40ae56d3ef">
        <p data-block-id="e28c32b4-2abe-460b-bb78-64f7ec383dcf">To manage the vSR, select and click
            <strong>ENROLL</strong>.</p>
    </li>
    <li data-block-id="17881f93-d655-41d0-a0af-c4be0d5857a4">
        <p data-block-id="0e66e52c-39e3-42b9-86dd-c9fd51719188">When enrolled, the vSR is managed on ZPE Cloud, the same
            as any other Nodegrid device.</p>
    </li>
</ol>
