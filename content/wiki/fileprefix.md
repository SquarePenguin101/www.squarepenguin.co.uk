## get_iplayer File Prefix Configuration

### Substitution Parameters

get_iplayer 2.83 introduced a slightly extended syntax for [substitution parameters](/wiki/documentation#substitution-parameters) used with the `--fileprefix` option.  It is now possible to define separators in `--fileprefix` that are omitted when the associated parameter is empty.  This should be of use to all get_iplayer users, but will be of particular value to XBMC/Plex users since scrapers expect particular formats for names of files to be automatically imported.

Consider this example setting in the user options file:

	fileprefix <nameshort>.<senum>.<episodeshort>

Each substitution parameter can now have the separator defined as a prefix inside the left angle bracket:

	fileprefix <nameshort><.senum><.episodeshort>

This signifies that the prefix will be omitted if the associated parameter value is empty.

**NOTE:** This new separator syntax is only useful with `<senum>` and `<episodeshort>` since all other metadata fields will almost always be populated.  The new syntax was implemented primarily to make it easier to create output file names compatible with XBMC scrapers.

Below are some examples showing how the output file prefix is altered by the changes in get_iplayer 2.83+.  OLD and NEW refer to pre- and post-2.83 behaviour, respectively.

1. The Painted Veil (film, series/episode numbers undefined)

		OLD: The_Painted_Veil..
		NEW: The_Painted_Veil

	Films don't have `<senum>` or `<episodeshort>` defined.

2. Turner's Thames (non-film, series/episode numbers undefined)

		OLD: Turners_Thames..
		NEW: Turners_Thames.s01e01

	Non-film programmes that are one-offs (e.g., standalone documentaries) don't have `<senum>` or `<episodeshort>` defined. Series and episode numbers are forced to 1 in order to distinguish them from films.

3. Dancing on the Edge (non-film, series number undefined)

		OLD: Dancing_on_the_Edge.s00e01.Episode_1
		NEW: Dancing_on_the_Edge.s01e01.Episode_1

	TV series that are one-offs or have yet to be recommissioned don't have a series number, so it is forced to 1. This should prevent XBMC from identifying them as one-off specials.

4. Silent Witness (non-film, episode number undefined)

		OLD: Silent_Witness.s16e00.Change_Part_1
		NEW: Silent_Witness.s16e00.Change_Part_1

	There is no difference since when get_iplayer can determine the series number but can't determine an episode number, there is no way to select an arbitrary value for the latter. It must be fixed manually.

### Dates in Episode Names

Some programmes (EastEnders, for example) have episode names that contain only the date of broadcast in UK short format: dd/mm/yyyy.  By default, the date will be interpolated into the name of the output file as yyyy-mm-dd.  XBMC/Plex scrapers may only be able to recognise a date in that format. If you do not wish to convert dates for some reason, use the `--no-isodate` option **[DEPRECATED]**.

### Zero-padding in `<episodenum>` and `<seriesnum>`

In `--fileprefix` or `--subdir-format`, you can now use parameters in the form `<00episodenum>` or `<00seriesnum>` to produce values padded with zeroes. Padded string width is determined by number of zeroes, so the above would pad "5" to "05". If you are also using an optional prefix character, it must come before the padding indicator, e.g., `<.00episodenum>`.  Zero-padding is supported in get_iplayer 2.86+.
