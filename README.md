### Introduction

This is a simple script to use the CDYNE SMS service to send Nagios pages.


### Instructions

1. Copy the sms file to /usr/bin/local/sms
2. Edit the `outgoing_did` and `cdyne_sms_key` values
3. Set your Nagios commands.cfg file similar to this:

```nagios
# 'notify-service-by-sms' command definition
define command{
  command_name	notify-service-by-sms
	command_line	/usr/bin/printf "%b" "$NOTIFICATIONTYPE$\nService: $SERVICEDESC$\nHost: $HOSTALIAS$\nAddress: $HOSTADDRESS$\nState: $SERVICESTATE$\nDate/Time: $LONGDATETIME$\n\n$SERVICEOUTPUT$\n" | /usr/local/bin/sms $CONTACTADDRESS1$
	}


# 'notify-host-by-sms' command definition
define command{
	command_name	notify-host-by-sms
	command_line	/usr/bin/printf "%b" "$NOTIFICATIONTYPE$\nHost: $HOSTNAME$\nState: $HOSTSTATE$\nAddress: $HOSTADDRESS$\nInfo: $HOSTOUTPUT$\n\nDate/Time: $LONGDATETIME$\n" | /usr/local/bin/sms $CONTACTADDRESS1$
	}

```
