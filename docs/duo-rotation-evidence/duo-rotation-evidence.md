# Duo split-view rotation evidence

## A. Uninterrupted physical control

Poki 0.4.1 build 1360 on iOS 27.2.1. The local build included the workspace launcher fix. The exact commit for this development build was not embedded and is unverified.
Safari and an empty test note were side by side in landscape. The task dispatched once. The destination showed one image on visual readback, and the saved task reported success.

## B. Physical rotation during drag

Poki 0.4.1 build 1361, tree 245b995d7593ceab5d5f5f0ef682d9c93d68630e, PR revision 338695205567dd2baadfd6add818027b225defea.
The operator turned the unfolded device to portrait while the picture was moving. The saved task contains one drag call. That call reports "sent" and a failed immediate pane confirmation. On return to landscape, Poki verified the pair again and then read the destination. The test note was empty below its title. Zero images were visible and no second drag was dispatched.

The following lines are from the matching physical run. Wall-clock times and unrelated activity have been removed.

```
[agent] started: Drag
[chat] Split View changed; waiting to read the workspace again
[chat] Split View restored; the model received a fresh pane read
[runner] finish: both apps stay open in Split View
```

The report of zero images is visual readback from this run. The retained evidence for this case is the saved task and this log excerpt.

## C. Already-landed scenario, automated on the Duo simulator

Build 1363, tree 9e4e6338dfa89f9becbe2f87869d176a5d903df0. The chat test testSplitViewChatInspectsTheDestinationAfterRotationDuringAnImageDrop injects a layout change after dispatch and returns one attachment in the destination read. The scripted model requests another drag, which is refused. The test asserts exactly one transport dispatch. This case uses an injected transport and does not establish physical delivery.

## D. Native simulator rotation and subsequent navigation

Build 1362, revision 3f746c163d795ed17ea46cf4b4721d70a8a7da1a, Duo simulator iOS 27.1. Device Hub rotated the actual Safari and Settings app windows. Poki suspended the next call in portrait and re-read both panes on return. The next input opened Settings > General > Screen Capture, confirmed by a fresh pane read. The session was saved.
