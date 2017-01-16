---
layout: post


title: Running Virtualbox VMS On Soyoustart Ubuntu Servers
author:
  display_name: austincode

  email: luke@austincodingacademy.com
  url: ''

author_email: luke@austincodingacademy.com
date: '2016-11-29 19:45:28 -0600'
date_gmt: '2016-11-29 19:45:28 -0600'
categories:
  - Learn to Code
  - Advanced
tags: []
comments: []
---

By Joe McCullough

After installing Ubuntu on my [SoYouStart](https://www.soyoustart.com/us/) machine (amazing machines for the price by the way), the first thing I did was attempt to install [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

After attempting to run vagrant up, I was greeted with the following error:[/cs_text][/cs_column][/cs_row][cs_row inner_container="true" marginless_columns="false" style="margin: 0px auto;padding: 0px;"][cs_column fade="false" fade_animation="in" fade_animation_offset="45px" fade_duration="750" type="1/1" style="padding: 0px;"][x_code]~/vms/server$ vagrant up
VirtualBox is complaining that the installation is incomplete. Please
run `VBoxManage --version` to see the error message which should contain
instructions on how to fix this error.[/x_code][/cs_column][/cs_row][cs_row inner_container="true" marginless_columns="false" style="margin: 0px auto;padding: 0px;"][cs_column fade="false" fade_animation="in" fade_animation_offset="45px" fade_duration="750" type="1/1" style="padding: 0px;"][cs_text]THE PROBLEM ORIGIN
The origin of the problem is likely that the server was built on a custom kernel. You can verify this by executing the following command:

`$ uname -r`
If your server was built using the official kernel, it would be of the following form:

`3.13.0-45-generic`
However, the output of the command in my case was

`3.14.32-xxxx-grs-ipv6-64`

**THE PROBLEM SOLUTION**
Unfortunately, the easiest way to alleviate the issue is to rebuild the server from the SoYouStart dashboard using the correct configuration options. This will involve completely wiping your server, so be sure to back up any data you've placed on the server thus far.

**REBUILDING THE SERVER**
First, head to your server dashboard. Then click the "Reinstall" button on the top right.

Choose your desired Ubuntu version. Be sure to check "Custom installation". Click Next.Unless you have any desire to adjust the partitioning scheme, just check "Yes" beside the **Do you want to install it solely on the first disk?** prompt. Click Next.Here, you may optionally customize the hostname if you wish. Leaving the hostname field blank is fine as well.

If you have uploaded an SSH key to your account, you can specify have your SSH keys installed onto the server when its built. (You can access the SSH Keys settings by clicking your name in the top right in the dashboard and selecting SSH Keys). If you do not use SSH keys, SoYouStart will send you an email with the root password once the server has finished building. You can leave the two remaining Post Installation fields blank.

Now, the part we've been waiting for. Be sure to check the **Use the distribution Kernel** check box. Then click Next.You will be asked to review and confirm.**VERIFYING THE BUILD**
After the server rebuilds and you can SSH into the machine, verify the kernel version is of the right form.

`$ uname -r 3.13.0-45-generic`
At this point, you should be able to successfully install VirtualBox and Vagrant on your server.

Have fun building!
