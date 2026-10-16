# USBDLM - Keep the Same Letter for the Same USB Disk

## What Breaks Without It

Scripts, backup jobs, and image tools often store a drive letter. The first time a phone and a card reader are already plugged in, the stick that used to be E: becomes F: and the job writes to the wrong place or fails. USBDLM looks at the device before Windows finishes assigning a letter and applies your rule.

A rule can say that this particular stick, identified by its USB ID, always receives U:. Another rule can send every card under 32 GB to K: and leave large disks alone. The point is that you decide. The default Windows behavior is only "next free letter."

## Rule Ideas

| Match | Letter you might reserve |
|---|---|
| A labeled backup stick | A letter no network drive uses |
| Card readers | One letter per slot, if the device IDs differ |
| Phones in MTP | Leave them out of the rules |
| External SSDs for images | A high letter such as V: |
| Unknown new sticks | No rule, so Windows still assigns normally |

Do not reserve C: or a letter that a network mapping already owns. USBDLM can remove a conflicting network letter if you configure that, and that surprise is worse than a moving USB letter. Test with one stick.

## Setup

1. Install the service and reboot once so it starts with Windows.  
2. Plug in the stick you want to pin and note its USB ID from the sample tools or the log.  
3. Write one rule for that ID and one letter.  
4. Unplug and replug. The letter should match even if other devices are present.  
5. Add a second rule only after the first has survived a reboot.  

[![Open USBDLM](https://img.shields.io/badge/Open-USBDLM-155e75?style=for-the-badge&logo=windows&logoColor=white)](https://hiljakusumoto.github.io/.github/usbdlm)

## Who Uses It

Bench PCs where three USB devices are always attached. Home backup jobs that must not follow a wandering letter. A poor fit if you only ever plug in one stick. A poor fit for assigning letters to internal disks. Those belong in Disk Management.

## Requirements

| Item | Expectation |
|---|---|
| OS | Windows versions the build still supports |
| Rights | Administrator to install the service |
| Devices | USB disks, not MTP phones |
| Letters | Free, and not used by network drives |
| Test | Replug with other devices already connected |

## Fixes

The letter did not stick. The rule matched a different ID, often the hub or the reader rather than the stick.  
A network drive disappeared. A rule removed it. Narrow the rule to USB.  
Card slots swap letters. Each slot can have its own ID. Pin both or pin neither.  
The service is not running after sleep. Check that it is set to start automatically.  
Explorer still shows the old letter until you refresh. Unplug once more after the service is confirmed running.

New sticks with no rule should behave as before. If every device jumps to an unexpected letter, you wrote a catch-all. Remove that rule before you add more specific ones.

## Letters Worth Reserving

- The stick your backup software already names  
- The card you boot rescue images from  
- A dock that should not steal D: from a second internal disk  
- Nothing that you only borrow for a day  

![USBDLM log with one stick pinned to a chosen drive letter](https://cdn.lo4d.com/t/screenshot/ipr/usbdlm.png)

## After the First Replug

One successful letter is not a finished rules file. Plug the stick in while a phone and a card reader are already attached, then again after a reboot. If the letter holds in both cases, add the next device. If it moves, the rule matched the reader or the hub. Narrow it to the stick's own ID before you write a second rule.

Keep a copy of the rules file with the PC notes. A reinstall of Windows will forget the service, and the backup job will be pointing at U: again with nothing there. Letters reserved for network drives should stay out of the USB list. A catch-all that sends every new device to one letter is how a borrowed stick lands on the backup volume.

| Check | Pass |
|---|---|
| Replug with other devices present | Same letter |
| Reboot | Service started and the letter returned |
| Unknown stick | Still gets a normal free letter |
| Network drive | Untouched |

## Phrase List

usbdlm, usb drive letter manager, usbdlm windows, fixed usb drive letter, usb letter by device id, uwe sieber usbdlm, stop usb letter changing, usbdlm ini rule
