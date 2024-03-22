# Archivators

tar.gz archives:

```
# Create:
tar -czvf archive.tar.gz dir1 dir2 file1.txt file2.txt
# Extract:
tar -xzvf archive.tar.gz

# Split tar.gz into the chunks of specific size:
tar -czf archive.tar.gz dir1 dir2 | split -b 1G - archive.tar.gz.part.
# Convert back to single tar.gz file:
cat archive.tar.gz.part.* | tar -xz
```

zip archive:
```
# Create recursively
zip -r archive.zip /path/to/dir
```
