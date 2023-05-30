#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>

int countFilesInDirectory(const char* path)
{
    DIR* directory;
    struct dirent* entry;
    struct stat fileStat;
    int count = 0;

    if ((directory = opendir(path)) == NULL)
    {
        printf("Error opening DIR: %s\n", path);
        return -1;
    }

    while ((entry = readdir(directory)) != NULL)
    {
        char filePath[512];
        sprintf(filePath, "%s/%s", path, entry->d_name);

        if (stat(filePath, &fileStat) == 0 && S_ISREG(fileStat.st_mode))
        {
            count++;
        }
        else if (stat(filePath, &fileStat) == 0 && S_ISDIR(fileStat.st_mode) && strcmp(entry->d_name, ".") != 0 && strcmp(entry->d_name, "..") != 0)
        {
            count += countFilesInDirectory(filePath);
        }
    }

    closedir(directory);
    return count;
}

int main(int argc, char* argv[])
{
    const char* path;

    if (argc > 1)
    {
        path = argv[1];
    } else
    {
        path = ".";
    }

    int fileCount = countFilesInDirectory(path);

    if (fileCount >= 0)
    {
        printf("Files in DIR '%s': %d\n", path, fileCount);
    }

    return 0;
}



