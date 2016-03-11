# Introduction

LogToMail automatically sends e-mails when specific Windows events are raised on any Windows computer running a server or client version of Windows.

LogToMail runs either as a Windows service or as a console application. Both setup and configuration are straightforward.

It is extremely helpful to monitor specific events on your servers, or your customers' servers without deploying full fledge monitoring or management software.

As soon as LogToMail is up and running, it monitors Windows events. When an event matching the defined criteria is raised, an email is sent to the configured recipients.

By default, LogToMail catches all errors, ignoring warning and other messages. But you can define your own rules to send emails only when specific events happen, such as errors of your own application, or system warnings except those that you know.

This document describes how to install and uninstall LogToMail, as well as how to use it.