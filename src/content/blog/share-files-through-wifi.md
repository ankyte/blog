---
author: Ankit Sahu
pubDatetime: 2023-05-15T00:00:00Z
title: Effortlessly Share Files Across Devices on Your Wi-Fi Network with Python
postSlug: share-files-through-wifi
featured: false
draft: false
tags:
  - python
  - network
description: Are you tired of using USB drives or sending files over email to share files between your devices on the same Wi-Fi network? Well, there's an easier way! In this post, I'll show you how to share files wirelessly between devices on the same Wi-Fi network using Python.
---

Are you tired of using USB drives or sending files over email to share files between your devices on the same Wi-Fi network? Well, there's an easier way! In this post, I'll show you how to share files wirelessly between devices on the same Wi-Fi network using Python.

## Table of contents

Are you tired of using USB drives or sending files over email to share files between your devices on the same Wi-Fi network? Well, there's an easier way! In this post, I'll show you how to share files wirelessly between devices on the same Wi-Fi network using Python.

Python comes with a built-in module called `http.server` that allows you to serve files over HTTP. By running a simple command in your terminal, you can turn your computer into a file server that other devices on the same Wi-Fi network can connect to and download files from.

## Here are the steps to share files using Python:

Step 1: Open your terminal or command prompt.

Step 2: Navigate to the folder that contains the file you want to share.

Step 3: Run the following command:

```bash
python -m http.server
```

This will start a simple HTTP server on your computer that serves files from the current directory.

Step 4: Open a web browser on another device that is connected to the same Wi-Fi network.

Step 5: In the address bar, enter the IP address of the computer that is running the file server, followed by the port number that the server is listening on.

Use **ipconfig getifaddr <interface name>** command to find ip address

Example

```bash
http://192.168.1.100:8000
```

Replace `192.168.1.100` with the IP address of your computer, and `8000` with the port number that the server is listening on (which is usually `8000` by default).

Step 6: Press Enter, and you should see a list of files and folders that are in the directory that you ran the `http.server` command in.

Step 7: Click on the file that you want to download, and it will be downloaded to the device that you are using.

That's it! You can now share files wirelessly between devices on the same Wi-Fi network using Python.

One thing to keep in mind is that the file server that `http.server` creates is not secure, and anyone on the same Wi-Fi network can access it. So, make sure to only share files that you don't mind other people seeing.
