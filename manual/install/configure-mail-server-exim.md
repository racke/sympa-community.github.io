---
title: 'Configure mail server: Exim'
up: configure-mail-server.md
next: configure-mail-server-opensmtpd.html
---

Configure mail server: Exim
===========================

Requirements
------------

  * [Exim](https://www.exim.org/).

  * A mail domain name for the mailing list service.
    See also "[Requirements](../requirements.md#network-requirements)".

    In the instructions below, ``mail.example.org`` will be used for example.

Using virtual domains
---------------------

Add a router for your lists to the Exim configuration:

    sympa_aliases:
      driver = redirect
      allow_defer
      allow_fail
      domains = dsearch;/etc/exim4/sympa
      data = ${expand:${lookup{$local_part}lsearch*@{/etc/exim4/sympa/$domain}}}
      retry_use_local_part
      user = sympa
      group = sympa
      pipe_transport   = address_pipe
      file_transport   = address_file
      no_more
