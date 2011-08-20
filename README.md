There are two scripts here: `movies-maintenance`, and `tv-maintenance`. I wrote them to help ensure my collection of TV shows and movies collections organized.  The scripts are intended to be interactive; so they're not really well-suited for use as a _cron_ job.  I only run them after I have ripped a new disc into the collection, as at no other time should the files change.

They are written in Ruby, and I use them on MRI 1.9.2. YMMV if you use them on a different version.

# Movies

This script aims to organize your film collection using the following format:

```
movies
├── by-name
│   ├── 12 Monkeys [1995].avi
│   ├── Clerks [1994].avi
│   ├── Clerks 2 [2006].avi
│   ├── Heat [1995].avi
│   ├── Muppet Treasure Island [1996].avi
│   ├── Star Wars 1 - The Phantom Menace [1999].avi
│   ├── Star Wars 2 - Attack of the Clones [2002].avi
│   ├── Star Wars 3 - Revenge of the Sith [2005].avi
│   ├── Star Wars 4 - A New Hope [1977].avi
│   ├── Star Wars 5 - The Empire Strikes Back [1980].avi
│   ├── Star Wars 5 - The Empire Strikes Back [1980].jpg
│   ├── Star Wars 6 - Return Of The Jedi [1983].avi
│   ├── Star Wars 6 - Return Of The Jedi [1983].jpg
│   ├── The Blues Brothers [1980].avi
│   ├── The Boondock Saints [1999].avi
│   ├── The Dark Knight [2008].avi
│   ├── The Godfather [1972].avi
│   ├── The Godfather 2 [1974].avi
│   ├── The Godfather 3 [1990].avi
│   ├── The Score [2001].avi
│   ├── The Score [2001].nfo
│   ├── V for Vendetta [2005].avi
│   ├── XMen Origins - Wolverine [2009].avi
│   ├── XXX [2002].avi
│   └── Zombieland [2009].avi
└── by-date
    ├── 1972_The Godfather.avi -> ../by-name/The Godfather [1972].avi
    ├── 1974_The Godfather 2.avi -> ../by-name/The Godfather 2 [1974].avi
    ├── 1977_Star Wars 4 - A New Hope.avi -> ../by-name/Star Wars 4 - A New Hope [1977].avi
    ├── 1980_Star Wars 5 - The Empire Strikes Back.avi -> ../by-name/Star Wars 5 - The Empire Strikes Back [1980].avi
    ├── 1980_The Blues Brothers.avi -> ../by-name/The Blues Brothers [1980].avi
    ├── 1983_Star Wars 6 - Return Of The Jedi.avi -> ../by-name/Star Wars 6 - Return Of The Jedi [1983].avi
    ├── 1990_The Godfather 3.avi -> ../by-name/The Godfather 3 [1990].avi
    ├── 1994_Clerks.avi -> ../by-name/Clerks [1994].avi
    ├── 1995_12 Monkeys.avi -> ../by-name/12 Monkeys [1995].avi
    ├── 1995_Heat.avi -> ../by-name/Heat [1995].avi
    ├── 1996_Muppet Treasure Island.avi -> ../by-name/Muppet Treasure Island [1996].avi
    ├── 1999_Star Wars 1 - The Phantom Menace.avi -> ../by-name/Star Wars 1 - The Phantom Menace [1999].avi
    ├── 1999_The Boondock Saints.avi -> ../by-name/The Boondock Saints [1999].avi
    ├── 2001_The Score.avi -> ../by-name/The Score [2001].avi
    ├── 2002_Star Wars 2 - Attack of the Clones.avi -> ../by-name/Star Wars 2 - Attack of the Clones [2002].avi
    ├── 2002_XXX.avi -> ../by-name/XXX [2002].avi
    ├── 2005_Star Wars 3 - Revenge of the Sith.avi -> ../by-name/Star Wars 3 - Revenge of the Sith [2005].avi
    ├── 2005_V for Vendetta.avi -> ../by-name/V for Vendetta [2005].avi
    ├── 2006_Clerks 2.avi -> ../by-name/Clerks 2 [2006].avi
    ├── 2008_The Dark Knight.avi -> ../by-name/The Dark Knight [2008].avi
    ├── 2009_XMen Origins - Wolverine.avi -> ../by-name/XMen Origins - Wolverine [2009].avi
    └── 2009_Zombieland.avi -> ../by-name/Zombieland [2009].avi
```

Files are placed in the `by-name` directory, then the script creates symbolic links in the `by-date` directory, placing the year first (and asking for the year if it's not already there), in order to facilitate quick sorting/browsing by date instead of name. Since I store these files on my home file server, and access them via Samba and NFS, it's helpful not to have to wait for the operating system to fetch metadata before I can sort by year.  When I use software like Boxee, or similar, that scan your library, I make sure to prevent from seeing the `by-date` directory, so I don't have duplicates. 

# TV

I aim to organize my TV shows in the following structure:

```
./Show Title/s1/Show Title_1x01_Episode Title.ext
```

Often, when I am ripping a new set of DVDs to disk, I'll do the whole season in batch, giving them simple names (ep1.avi, ep2.avi, etc...). When the ripping is complete, I'll use my trusty pyRename to give them the format above, excluding the episode names. I'll copy it to my file server, and then run the script. Then the script will do the renaming for me; it will ask for a title for any episode that is missing one. It will also scan new and current titles to ensure Windows filename validity (since I need to share with Windows clients), making adjustments as neccesary.

Extra files, like subtitles, images (see [my video-gallery script](http://github.com/rtlong/video-gallery)), meta-data (*.nfo), etc., are handled in the same breath. If the name matches it's episode (except, of course, for the extension) when the script finds it, it will be renamed accordingly.


