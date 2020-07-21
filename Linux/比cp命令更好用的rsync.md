比cp命令更好用的rsync

拷贝整个目录的同时不拷贝某些文件

rsync -av --progress tenant-product-admin servier-admin --exclude tenant-product-admin/node_modules


前端项目 copy, 去掉 node_modules

$ man rsync 
...
	-a, --archive               archive mode; same as -rlptgoD (no -H)
        --no-OPTION             turn off an implied OPTION (e.g. --no-D)
	-v, --verbose
	-h, --human-readable        output numbers in a human-readable format
        --progress              show progress during transfer
    -P                          same as --partial --progress
...

