---
layout: default
---

# Attachments

## Introduction

Matroska supports storage of related files and data in the Attachments Top-Level Element. Attachments can be used to store related cover art, font files, transcripts, reports, error recovery files, picture or text-based annotations, copies of specifications, or other ancilliary files related to the Segment.

`Matroska Readers` MUST NOT execute files stored as Attachments.

## Cover Art

This section defines a set of guidelines for the storage of cover art in Matroska files. A `Matroska Reader` MAY use embedded cover art to display a representation still-image depiction of the multimedia contents of the Matroska file.

Cover art SHOULD only use the JPEG and PNG picture formats.

There can be 2 different covers for a movie/album. A portrait one (like a DVD case) and a landscape one (like a banner ad for example, looking better on a wide screen).

There can be 2 versions of the same cover, the `normal cover` and the `small cover`. The dimension of the `normal cover` SHOULD be 600 on the smallest side (for example, 960x600 for landscape, 600x800 for portrait, or 600x600 for square). The dimension of the `small cover` SHOULD be 120 on the smallest side (for example, 192x120 or 120x160).

Versions of cover art can be differentiated by the filename, which is stored in the `FileName Element`. The default filename of the `normal cover` in square or portrait mode is `cover.(jpg|png)`. When stored, the `normal cover` SHOULD be the first Attachment in storage order. The `small cover` SHOULD be prefixed with "small_", such as `small_cover.(jpg|png)`. The landscape variant SHOULD be suffixed with "_land", such as `cover_land.(jpg|png)`. The filenames are case sensitive and SHOULD all be lower case.

The following table provides examples of file names for cover art in Attachments.

FileName             | Image Orientation  | Pixel Length of Smallest Side
---------------------|--------------------|------------------------------
cover.jpg            | Portrait or square | 600
small_cover.png      | Portrait or square | 120
cover_land.png       | Landscape          | 600
small_cover_land.jpg | Landscape          | 120

## Font files

Font files MAY be added to a Matroska file as Attachments so that the font file may be used to display an associated subtitle track. This allows the presentation of a Matroska file to be consistent in various environments where the needed fonts might not be available on the local system.

To associate a font file with a subtitle track, the font file MUST be stored as an Attachment within the same Segment. The `TrackEntry Element` of the associated subtitle track SHOULD store an `AttachmentLink Element` that contains the value of the `FileUID Element` of the `AttachedFile Element` that stores the font file.

For subtitle formats that reference a required font by name, such as SubStation Alpha (SSA/ASS), the `AttachmentLink Element` is RECOMMENDED. If no `AttachmentLink Element` is used then the Matroska Reader SHOULD use the font(s) stored in Attachments that match the names of those needed by the subtitle encoding. If the subtitle encoding requires fonts that are not specified by an `AttachmentLink Element` or use names that do not match the `FileName` of any `AttachmentFile Elements` then the Matroska Reader SHOULD attempt to find a system font to use with the subtitle track.
