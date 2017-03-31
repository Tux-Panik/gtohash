# gtohash
Provide useful details about a file or couple of files from current folder
Query include hidden files.

1°/ Just add the following code to your .bashrc file:


```#GTOHASH FILE DETAILS FUNCTION:
function gtohash() {
                lvl=$1
                ext=$2
                for files in `find -maxdepth $lvl -type f -iname "*$ext"`
                do
                        echo -ne 'File:    ' && echo "$files"
                        echo -ne 'Path:    ' && pwd
                        echo -ne 'Type:    ' && file -b "$files"
                        echo -ne 'Access:  ' && stat -c %x "$files" | cut -d. -f1
                        echo -ne 'Modif.:  ' && stat -c %y "$files" | cut -d. -f1
                        echo -ne 'Size:    ' && du -h "$files" | cut -d '       ' -f1
                        echo -ne 'MD5:     ' && md5sum "$files" | awk '{ print  $1 }'
                        echo -ne 'SHA-1:   ' && sha1sum "$files" | awk '{ print $1 }'
                        echo -ne 'SHA-256: ' && sha256sum "$files" | awk '{ print $1 }'
                        echo -ne 'SHA-512: ' && sha512sum "$files" | awk '{ print $1 }'
                        echo ""
                done
                 }```


2°/ Reload your .bashrc file, using
`source ~/.bashrc`


Usage:

gtohash [depth] [file]
Depth = integer. 1 is current directory.
File = in a precise file or .ext or all files (if nothing is specified as second argument)

Examples:
gtohash 1 my_interesting_file.txt
gtohash 2 .exe
gtohash 50
