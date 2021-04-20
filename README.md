# dir2fat32-esp

This is a forked version of https://github.com/Othernet-Project/dir2fat32 which
has the following differences:

- `dir2fat32.sh` is renamed to `dir2fat32-esp`
- It makes a GPT partition table rather than MBR
- It creates a single EFI system partition formatted as FAT32
- Misc improvements

dir2fat32-esp creates a disk image with a single FAT32 EFI system partition
from the contents of a directory, without mounting or root privileges,
completely automatically.

## Prerequisites

dir2fat32-esp requires the following packages to be installed on the host Linux
system:

- util-linux (`fdisk`)
- dosfstools (`mkfs.fat`)
- mtools (`mmd`, `mcopy`)

## Quick usage guide

Before running the script, you need to prepare the source directory. The
directory should not contain any symlinks or paths with characters that are
illegal on FAT32. Note that file and directory permissions do not really
matter.

Once the directory is prepared, invoke the dir2fat32-esp script:
```
$ ./dir2fat32-esp test.img 200 test
==============================================
Output file:      test.img
Partition size:   200 MiB
Image size:       208 MiB
Sector size:      512 B
Source dir:       test
==============================================
===> Creating container image
===> Creating FAT32 partition image
===> Copying files
  Creating hardware
  Copying bash_functions.sh
  Copying aliases_example.txt
  Copying colors.sh
  Copying alias_manager.sh
  Copying hardware/backlight.sh
  Copying README.rst
===> Copying partition into container
===> Removing partition image file
===> DONE
```

The above example creates an image file called `test.img` that is 208 MiB in
size and contains the contents of the `test` directory.

The image has a GPT partition table with a single FAT32 partition.

## License

This script is released under GNU GPLv3. See the ``COPYING`` file for more
details or visit `<http://www.gnu.org/licenses/>`.
