---
title: Messages
description: Working with ZeroMQ messages
toc: true
weight: 3
---

{{% capture overview %}}

A ZeroMQ message is a discrete unit of data passed between applications or
components of the same application. From the point of view of ZeroMQ itself
messages are considered to be opaque binary data.

On the wire, ZeroMQ messages are blobs of any size from zero
upwards that fit in memory. You do your own serialization using protocol
buffers, msgpack, JSON, or whatever else your applications need to speak. It's
wise to choose a data representation that is portable, but you can make your own
decisions about trade-offs.

The simplest ZeroMQ message consist of one frame (also called message part).
Frames are the basic wire format for ZeroMQ messages. A frame is a
length-specified block of data. The length can be zero upwards. ZeroMQ
guarantees to deliver all the parts (one or more) for a message, or none of
them. This allows you to send or receive a list of frames as a single
on-the-wire message.

A message (single or multipart) must fit in memory. If you want to send files of
arbitrary sizes, you should break them into pieces and send each piece as
separate single-part messages. Using multipart data will not reduce memory
consumption.

{{% /capture %}}

## Working with strings

Passing data as strings is usually the easiest way to get a communication going
as serialization is rather straightforward. For ZeroMQ we established the rule
that **strings are length-specified and are sent on the wire without a trailing
null**.

{{< example messages_strings_send_recv >}}

Because we utilise the frame's length to reflect the string's length we can send
mulitple strings by putting each of them into a seperate frame.

{{< example messages_strings_send_recv_multi >}}

## More

Find out more about working with messages:

{{< example messages_functions >}}
