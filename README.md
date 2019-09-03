# Test Application for the RTC and NVRAM Tibbit (#42)

You will need:

- TPP2, TPP2(G2), TPP3, or TPP3(G2) board
- One Tibbit #42
- Optionally, one Tibbit #9 or #10 (12V->5V regulator)
- Optionally, one Tibbit #18 (power jack)

*The last two Tibbits are necessary if you are going to power your rig from a 12V power adaptor. Alternatively you can supply regulated +5V power directly to the TPP.*

Tibbit #42 is based on the DS3234 high-precision RTC from Maxim Integrated.

This Tibbo BASIC project has several test modes. The desired mode is selected in the following line of code in main.tbs:

test_item=test_item=TEST_NVRAM '<<====================== SELECT DESIRED TEST CASE HERE

Tests are meant to be run in the debug mode as most test cases rely on sys.debugprint.

TEST_RTC_SET mode sets the RTC to the specified date and time. We understand it looks a bit strange that you need to manually set the clock. Obviously, there are ways to obtain the current data/time from the internet. Our rationale is that this is a simple test project, not a complete application. We didn't want to clutter the app with code that is not directly related to testing the RTC Tibbit.

The next test mode — TEST_RTC_GET — will repeatedly print the current date and time using the sys.debugprint method.

TEST_ALARM_EVERY_SEC will demonstrate the RTC's ability to trigger periodic alarms. In this test the alarm will be programmed to trigger every second. The code will wait until the -INT/MISO line is set LOW, thus indicating that the alarm has happened. The program will then print the current date/time and start waiting for the next alarm.

TEST_ALARM_EVERY_MIN is like the previous test, but the alarm will trigger every minute.

TEST_ALARM_AT_PRESET_DATE_TIME demonstrates yet another alarm feature of the DS3234 — the ability to trigger alarm once at preset date and time. This test will read the current date/time, then set the date/time alarm to trigger one minute later.

TEST_TEMP will repeatedly print the current temperature measured by the IC.

Finally, TEST_NVRAM will perform a write-and-read-back test of the IC's non-volatile RAM.