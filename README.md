> Mirror of [iceanimations/slatemaker](https://github.com/iceanimations/slatemaker), published by the
> studio under EPL 2.0. Kept here for reference; the original repository is the canonical one.

# slatemaker

Slate generation for shots in Hiero and Nuke Studio.

A slate is the card at the head of a shot telling a reviewer what they are about to watch: production,
episode, sequence, shot, version, artist, take. Hand-typed, it is wrong at least once a day. `slatemaker`
reads that information from the Hiero timeline instead, where the clip names already carry it, and builds
the slate clip from them.

## How it works

For each selected shot, the tool looks one frame before the shot's timeline-in for a clip named
`<shot>_Slate`. If it exists, that is the slate. If not, it is created, and the shot's metadata is
written into it as overlay text effects (`overlayTexts` reads them back out of the clip). Tags carry
the per-shot data, so the tool can tell a slate clip from a picture clip by name and position alone,
without a side database.

Settings are held in `QSettings` through a small descriptor layer (`slateMakerSettings.py`), so move
and display preferences survive across sessions.

## The modules

| File | Job |
|---|---|
| `slateMaker.py` | `Slate`, `SlateTag` and `SlateMaker`: detection, naming, overlay text |
| `slateMakerDialog.py` | The Hiero panel |
| `slateMakerAction.py` | Menu action and selection handling |
| `slateMakerSettings.py` | Typed settings over `QSettings` |
| `slateProcessor.py` | Batch processing over selected clips |

This one is standalone apart from Hiero itself, which is why it is readable without the rest of the
pipeline around it. It is Python 2 and PySide, as Hiero was at the time.

## Authorship

38 commits between 2015 and 2021, all mine.

LICENSE
=======

Copyright 2021. Talha Ahmed. All rights reserved.

This work is licensed under the terms of Eclipse Public License - v 2.0.
For a copy see https://www.eclipse.org/org/documents/epl-2.0/EPL-2.0.txt
