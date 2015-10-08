---
title: Hashed Page Tables
author: Asger, Oskar & Ulrik
---
# Hashed Page Tables

A difference between hashed page tables and linear page tables is that hashed
page tables use a hash function to look up the position of stored pages.
Therefore the physical position of a page can no longer be determined by its
index in the table, unlike linear page tables. The physical position of the
page is stored together with the entry, which adds extra data to the table.

Another big difference is that hashed page tables only store valid page
entries, which is the driving force behind using them.

The hash algorithm used is usually the page number modulo the number of entries
in the table as the hash function should be very fast to calculate. Because of
this we have to be able to handle hash collisions. The MMU has a limited number
of entries for each hash bucket (Intel Itanium has 1 and PowerPC has 8). To
store more than this number of entries in the hash bucket, the excess entries
are stored in a linked list. Typically the hardware walker can't search
through these linked lists, so this is left for the OS to handle, when a page
fault happens.
