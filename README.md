### smartcard-reader

smartcard-reader turns your Android device (running Kitkat or later) into a
payment terminal or similar smartcard reader. It uses NFC to interact with a
contactless smartcard, either physical or emulated.

#### So What?

What exactly can smartcard-reader do for you?

(Note: If you are relatively new to NFC and card emulation, or you just want more
info, please read the "Background Info" section below first, and then come back
here!)

HCE relies heavily on the routing APDUs from contactless terminals to the correct
apps, whether they reside on the host processor or UICC-based secure element.
Routing is based on AID, or Application ID, which of course is meant to uniquely
identify each smartcard app/service. That is the identifier used by the terminal
to "select" the particular card app with which it wants to interact. (For example,
Visa credit is identified by AID A0000000031010, and MasterCard credit is known by
AID A0000000041010.)

As such, I use smartcard-reader for testing AID routes on HCE-enabled devices. I
do this by issuing "select" APDU commands from smartcard-reader and checking for
the appropriate responses from another NFC-paired device -- the device under test.
smartcard-reader can also be used to check which smartcard apps are present on
or off host.

When paired with a second device that has the smartcard-demo app installed (which
uses HCE to emulate a smartcard on the host processor), Demo mode can be used to
demonstrate HCE connectivity and HCE (over ISO-DEP) as an alternative to Android
Beam, which depends on NFC P2P mode (and SNEP over LLCP over NFC-DEP).

Read more about "application selection" and AIDs [here](http://en.wikipedia.org/wiki/EMV#Application_selection).

And, [here](http://www.cardwerk.com/smartcards/smartcard_standard_ISO7816-4.aspx)
is an ISO 7816-4 reference containing APDU commands including "select file".

#### Come again?

Just run smartcard-reader on one device, set the App/AID that you want to select,
and tap it against another device -- the device doing the card emulation. You can,
of course, also tap a physical smartcard. You can also add your own Apps/AIDs, and
modify the ones you've added.

#### Background Info

Skip this section if you're well versed in the world of NFC card emulation for
mobile devices!

Smartcards, also known as chip cards, can be contact, contactless, or a hybrid
of the two. The contact type of smartcard has a SIM-like contact-based chip (In
fact, a mobile SIM is a reduced size smartcard). The chip speaks a character- or
block-level protocol based on ISO 7816, and individual apps define command and
response protocols based on APDU messages, or Application Programming Data Units.

The contactless type of smartcard adds the NFC antenna and speaks an NFC protocol
called ISO-DEP, based on ISO 14443-4. Apps still send APDUs -- based on ISO 7816-4
-- on top of the NFC ISO-DEP layer.

Contactless martcard emulation is made possible by the card emulation function of
NFC, also known as CE mode. While it's most commonly known for its use in credit
card payments (eg. on an Android enabled smartphone through apps such as Google
Wallet), it has other useful applications such as building access, public transit
ticketing, student tracking, etc.

Prior to the Android Kitkat release, NFC card emulation relied on a hardware
secure element connected to the device's NFC controller. The secure element can be
part of the device's SIM card or it can be another embedded component. Either way,
it provides a secure environment for applets to run and to interact with
contactless smartcard readers (eg. payment terminals).

Kitkat introduced a new feature called HCE, or host-based card emulation, which
allows an Android app running on the host processor to have direct control over
CE mode interaction, ie. talking directly to smartcard readers without the use of
a hardware secure element component. The feature also includes compatibility with
the hardware secure element, so that one app may use "host" card emulation (HCE)
while another uses "offhost" (hardware secure element) card emulation.

In addition to all of this, Kitkat also enabled a dedicated "reader mode", so apps
can listen solely for smartcards without having to worry about the potential
interference of other NFC functions such as CE or P2P (peer-to-peer) modes. This
new reader mode is a key enabler of smartcard-reader.

#### Screenshots

<img align="left" src="/docs/tn_screen_emv_read.png">

<img align="right" src="/docs/tn_screen_share_gmail.png">

<img align="left" src="/docs/tn_screen_select_mc.png">

<img align="right" src="/docs/tn_screen_parsed_select_rsp.png">

<img align="left" src="/docs/tn_screen_add_new_app.png">

<img align="right" src="/docs/tn_screen_manual_select.png">
