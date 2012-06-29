# Emacs wwtime

This library inserts a time of day with appropriate world-wide localization

I frequently arrange teleconferences with participants from several
time zones. In an effort to reduce confusion about the time of the
meeting, I try to publish the time in several relevant time zones.

But correctly calculating EST, PST, GMT, CET, and JST, for example,
requires too much thought. That's what computers are for. And since
I'm usually sending email reminders of the meeting time, that's
what Emacs is for.  And that's what this code is for.

## Usage

`(wwtime)`

wwtime will prompt for the time of day in the minibuffer. The time
entered will be inserted into the current buffer in each of the
time zones listed in wwtime-display. Note that the time can be
entered in any time zone, but will always be displayed in the time
zones listed in wwtime-display (and the time zone entered, even
if it is not a member of wwtime-display).

The time displayed will be followed by a + or - to indicate tomorrow
or yesterday (with respect to the time zone entered).

`(wwtime-convert)`

wwtime-convert prompts for a time of day and two time zones. It
converts the time from the first time zone to the second and displays
the result in the minibuffer.

## Example

Given the default settings, (wwtime) for "15:00 AKST" will insert:
"15:00AKST (07:00p EST, 04:00p PST, 00:00GMT+, 01:00CET+, 09:00JST+) "

## Customization

There are five customization variables. As of version 1.1, you can
set these with the Emacs customization feature. Wwtime is in the
"Convenience" group under M-x customize.

* `wwtime-time-zones` is the list of recognized time zones
* `wwtime-display` is the list of time zones to display
* `wwtime-ampm` is a list of time zones that use 12-hour am/pm format
* `wwtime-default-function` is the function that calculates the default time
* `wwtime-time-zone-aliases` maps long time zone names to one-word names

### Customization example

Here's the relevant section of my `~/.emacs` file, for example:

    (autoload 'wwtime "wwtime" nil t)
    (autoload 'wwtime-convert "wwtime" nil t)

    (setq wwtime-time-zones (append wwtime-time-zones '(("India" +5.5 "India"))))
    ;(setq wwtime-display '("EST" "PST" "GMT" "CET" "JST" "India"))
    ;(setq wwtime-display '("EDT" "PDT" "GMT" "BST" "CEST" "JST" "India"))
    (setq wwtime-display '("EDT" "PDT" "GMT"))
    ;(setq wwtime-display '("EST" "PST" "GMT"))
    (setq wwtime-ampm '("EST" "CST" "MST" "PST" "AKST"
                        "EDT" "CDT" "MDT" "PDT" "AKDT"
                        "India"))

I uncomment the relevant `wwwtime-display` settings depending on the season
of the year and the number of timezones involved in my telcons.
