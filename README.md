# MeetingNotes: install guide

MeetingNotes is a Mac app that records a meeting (your microphone and the sound playing on your Mac), turns it into a transcript with every line marked **Me** or **Them**, and lets you write your own notes beside it. It also writes AI notes from your notes and the transcript. Your meetings stay on your Mac; the audio and the text that your team's service needs to write the transcript and the AI notes are sent to it while you are signed in (exactly what, and where to: "What leaves your Mac", below).

This page is for the team. It covers installing, the first launch, the setup (sign in, your team, microphone, call audio, calendar), what the app asks macOS for and why, updating, and removing it. You do not need any account or password for a transcription or AI service: you sign in to your team once.

**You need:** a Mac with Apple Silicon (M1 or later) and macOS 14.2 or later. Intel Macs are not supported.

**Download:** the newest version is on the [Releases page](https://github.com/RahulSomaliya/meetingnotes-releases/releases/latest). Under **Assets**, get the file named `MeetingNotes-<version>-arm64.dmg`.

## Install

1. Open the downloaded `.dmg`.
2. Drag **MeetingNotes** onto **Applications** in the window that opens.
3. Eject the disk image (the eject button next to it in Finder's sidebar) and delete the `.dmg` if you like.

Optional check that the download is whole: the release also has a file ending in `.sha256`. Put both files in the same folder (for example Downloads), open Terminal there and run `shasum -a 256 -c MeetingNotes-<version>-arm64.dmg.sha256`. It should print `MeetingNotes-<version>-arm64.dmg: OK`.

## The first launch

MeetingNotes is signed by its author but **not notarized by Apple** (that needs a paid Apple developer account). macOS therefore blocks the first launch. This is expected; you allow it once, in System Settings.

1. Open **MeetingNotes** from Applications. macOS shows a message that it could not verify MeetingNotes (the exact wording depends on your macOS version). Click **Done**. Do not click **Move to Trash**.
2. Open **System Settings > Privacy & Security** and scroll down to the **Security** section. There is a line about MeetingNotes being blocked, with an **Open Anyway** button. Click it and confirm with your password or Touch ID.
3. Open MeetingNotes again. If macOS asks once more, click **Open**.

If the Open Anyway button is not there, open MeetingNotes from Applications once more, then go back to Privacy & Security: the button appears after a blocked try. (If macOS shows the button only for a limited time, repeat the blocked try.)

**Control-click > Open no longer works.** On macOS 15 and later that shortcut does not open an unidentified app any more; **Open Anyway** is the way.

### If macOS says the app is damaged, or Open Anyway never appears

A file downloaded in a browser carries a quarantine mark that makes macOS check it. If the steps above do not work, remove the mark from the copy in Applications. In Terminal:

```
xattr -dr com.apple.quarantine /Applications/MeetingNotes.app
```

This tells macOS "I got this file on purpose and I trust it", so it stops checking the app. Only do it for an app you got from this page, from someone you trust. Then open MeetingNotes again.

## Set up

The first time MeetingNotes opens, it fills the window with a short setup. A list of steps (**Sign in**, **Your team**, **Microphone**, **Call audio**, **Calendar**, **Done**) shows where you are. Do each once, in this order. You can open the same setup again later with **Set up** at the top of **Settings** (Settings is at the bottom of the sidebar); **Back to Settings** leaves it.

1. **Sign in.** On **Welcome to MeetingNotes**, in the **Team** card, press **Sign in**. Your browser opens your team's sign-in page; sign in there, then come back to MeetingNotes. If you closed the browser tab by mistake, press **Cancel** next to "Waiting for the browser…" and sign in again; if the browser did not open, press **Open it again**. With no internet, **Skip for now** goes on without signing in: recording and your own notes work, but there is no transcript and no AI notes until you sign in (Settings > Team).
2. **Your team.** Once you are signed in, a page called **Choose a team** appears only if you do not have a team yet, or have several and none is chosen. Pick yours: **Join team** on an invite, **Create a team**, or **Just me for now**. If your team is already chosen, this step passes by itself.
3. **Check your audio.** One page, two lines:
   - **Microphone.** Press **Allow**. macOS asks whether MeetingNotes may use the microphone; click **Allow**. This is your own voice, the **Me** side of the transcript. Press **Test microphone** and say a few words; the **Me** meter moves. The line then says **Ready**. If it says **Needs you** after you said no, press **Open System Settings** and switch MeetingNotes on under Microphone.
   - **Call audio.** This is the sound of the other people on the call, the **Them** side. Play a video or a sound on your Mac, then press **Test call audio**. macOS asks whether MeetingNotes may record the screen and system audio; click **Allow** (if macOS says MeetingNotes must quit and reopen, do that, then press **Test call audio** again). Within five seconds the **Them** meter moves and the line says "Call audio works." If it says "We could not hear the call", switch MeetingNotes on yourself in System Settings > Privacy & Security > Screen & System Audio Recording (the **Open System Settings** button goes there) and test again. MeetingNotes saves sound only, never a picture of your screen.

   Then press **Continue**. Nothing here is final: the page says "Redo it anytime in Settings."
4. **Remind me before meetings.** Optional. The switch uses your Apple Calendar to remind you a minute before a meeting (macOS asks once). Turn it on and press **Continue**, or press **Not now**.
5. **You're all set.** Press **Get started**.

That is all. MeetingNotes keeps each recording's audio for 30 days and your transcript and notes for good (a Mac that already had recordings before this version keeps their audio until you choose a number of days). When a call ends, MeetingNotes writes the AI notes for you; they never overwrite your own notes. **Regenerate** makes a new version and keeps the older ones.

## What MeetingNotes asks macOS for, and why

MeetingNotes asks only for what it needs, and only when you press the matching button. Each of these is one macOS dialog or one switch in System Settings; "if macOS shows" means the dialog depends on your macOS version and what you answered before.

| Permission | When it is asked | Why |
|---|---|---|
| **Microphone** | When you press **Allow** in the setup. If you skipped it, the first time you press **Record**. | Your own voice, the **Me** side of the transcript. The text macOS shows: "MeetingNotes records your microphone during meetings you start, so your own words appear in the transcript." Say no and the app records only the sound playing on your Mac, and tells you so. |
| **Screen & System Audio Recording** | When you press **Test call audio** in the setup. If you skipped it, the first time you record the sound playing on your Mac, if macOS shows a dialog. Otherwise you turn it on yourself: System Settings > Privacy & Security > Screen & System Audio Recording > MeetingNotes. | The other people on the call, the **Them** side. The text macOS shows: "MeetingNotes records the audio playing on this Mac during meetings you start, so the other people appear in the transcript." MeetingNotes saves audio only, never a picture of your screen. If it cannot hear the other side, the meeting shows **No sound from the call.** with an **Open System Settings** button. |
| **Calendar** | Only when you turn on **Remind me before meetings** in the setup, or **Remind me a minute before calendar meetings** in Settings > Meetings. | To remind you a minute before a meeting and to name its notes after it. The text macOS shows: "MeetingNotes reads your calendar to remind you a minute before a meeting and to name its notes. Your calendar never leaves this Mac." |
| **Automation** (control a browser) | Only if meeting detection checks a browser, the first time a browser such as Chrome or Arc starts using the microphone. One dialog per browser: "MeetingNotes wants access to control <browser>". | To read the address of the browser's open tab and ask about notes only when it is a meeting site such as Google Meet. Nothing is saved or sent. Say no and MeetingNotes asks about that browser's calls as before. You can turn this off with **Only ask for meeting sites in browsers** in Settings > Recording. |

Noticing that a call app is using the microphone needs no permission of its own, and MeetingNotes never records by itself: it asks first (**Take notes**, **Not now** or **Don't ask for** that app).

You can change any of these later in System Settings > Privacy & Security.

If macOS asks once whether "MeetingNotes Safe Storage" may use your login keychain (it keeps your sign-in safe), choose **Always Allow**.

## What leaves your Mac

Nothing, until you sign in to your team. After that:

- The **audio** of a recording goes to your team's service, which turns it into the transcript. Live transcript (the words appearing while you record) sends the audio as it is recorded.
- Your **notes and the transcript** go to your team's service when it writes AI notes.
- Your **calendar** never leaves your Mac.
- **Sharing** a meeting uploads its newest notes and gives you a link, only when you press **Share**.
- **Update check:** every few hours (and when you press **Check now**) MeetingNotes asks GitHub whether a newer version exists. GitHub sees your IP address and the app's name and version, like any web request. Nothing about you or your meetings is sent. Turn it off with **Check for new versions** in Settings > General; off means no request at all.

Signed out, nothing about a meeting leaves your Mac.

## Updating

When a newer version is out, MeetingNotes shows the new version in a few quiet places: a row above Settings in the sidebar ("Update available · Download X"), an item at the top of the menu bar menu ("Version X is ready"), and Settings > General (under Updates, where **Check now** looks right away). Nothing pops up and nothing changes while you record.

MeetingNotes never replaces itself. To update:

1. Click **Download** in the sidebar row (or in Settings > General). Your browser opens the release page; download the new `.dmg`.
2. Quit MeetingNotes (Command-Q, or **Quit MeetingNotes** in the menu bar menu; closing the window only hides it).
3. Open the new `.dmg`, drag **MeetingNotes** onto **Applications**, and choose **Replace**.
4. Open it. macOS may ask for **Open Anyway** again, as in the first launch; follow the same steps.

Your meetings, notes, recordings, sign-in and settings stay. The permissions above should stay too, because every version is signed with the same certificate; if macOS asks again, answer as before.

## Where your data lives

| What | Where |
|---|---|
| Meetings, notes, transcripts, AI notes, settings | `~/Library/Application Support/MeetingNotes/` (one database file) |
| Recordings (audio files) | `~/Library/Application Support/MeetingNotes/recordings/` |
| Your sign-in (kept encrypted) | `~/Library/Application Support/MeetingNotes/secrets/`; the item that unlocks it is in your login keychain ("MeetingNotes Safe Storage") |
| Logs (no notes, transcripts or sign-in details in them) | `~/Library/Logs/MeetingNotes/` (in the app: Help > Show Log Files) |
| Small app preferences | `~/Library/Preferences/com.rahulsomaliya.meetingnotes.plist` |

In Finder: **Go > Go to Folder…** (Shift-Command-G), then paste a path. MeetingNotes moves a recording's audio to the Trash after 30 days; the transcript and notes stay. You can change this with **Keep each recording's audio** in Settings > Recording (7, 30 or 90 days, or forever).

## Uninstall

1. Quit MeetingNotes (Command-Q, or **Quit MeetingNotes** in the menu bar menu).
2. Drag **MeetingNotes** from Applications to the Trash. This removes the app only; your meetings and recordings stay in the folders above.
3. To delete your data too, move `~/Library/Application Support/MeetingNotes`, `~/Library/Logs/MeetingNotes` and `~/Library/Preferences/com.rahulsomaliya.meetingnotes.plist` to the Trash. **This deletes every meeting, recording and note, and cannot be undone** once the Trash is emptied.
4. Optional: open **Keychain Access** and delete the "MeetingNotes Safe Storage" item. To forget the permissions you gave, run `tccutil reset All com.rahulsomaliya.meetingnotes` in Terminal (or switch MeetingNotes off in each pane of System Settings > Privacy & Security).

## Something does not work

- **MeetingNotes will not open, or says it is damaged:** the first-launch steps above; if Open Anyway never appears, the `xattr` line.
- **"No sound from the call." while a call is playing:** open System Settings > Privacy & Security > Screen & System Audio Recording and switch MeetingNotes on (the **Open System Settings** button goes there). Then record again.
- **"Your words will not be recorded: microphone access is off":** System Settings > Privacy & Security > Microphone, switch MeetingNotes on.
- **It asks you to sign in, or a transcript or AI notes do not appear:** open Settings > Team and press **Sign in** (step 1 above). If your browser does not open, press it again; if you are signed in and it still fails, your team's service may be down, so try again later.
- **Anything else:** tell the person who sent you this page. If you can, include the newest file in `~/Library/Logs/MeetingNotes/` (it contains no notes, transcripts or sign-in details, but read it before you send it).
