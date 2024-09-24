# soaical-media-web-app       

[24/09, 8:05 pm] +91 79952 47442: *EX7(a)*
#include<stdio.h>

int main() {
    int fragments[10], block[10], file[10], number_of_blocks, number_of_files;
    int temp, lowest = 10000;
    static int block_arr[10], file_arr[10];
    int m, n;

    // Input the total number of blocks
    printf("\nEnter the Total Number of Blocks:\t");
    scanf("%d", &number_of_blocks);

    // Input the total number of files
    printf("\nEnter the Total Number of Files:\t");
    scanf("%d", &number_of_files);

    // Input the sizes of the blocks
    printf("\nEnter the Size of the Blocks:\n");
    for(m = 0; m < number_of_blocks; m++) {
        printf("Block No.[%d]:\t", m + 1);
        scanf("%d", &block[m]);
    }

    // Input the sizes of the files
    printf("\nEnter the Size of the Files:\n");
    for(m = 0; m < number_of_files; m++) {
        printf("File No.[%d]:\t", m + 1);
        scanf("%d", &file[m]);
    }

    // Best Fit Allocation logic
    for(m = 0; m < number_of_files; m++) {
        for(n = 0; n < number_of_blocks; n++) {
            if(block_arr[n] != 1) {  // Check if the block is already allocated
                temp = block[n] - file[m];  // Calculate remaining space in the block
                if(temp >= 0) {  // Block can fit the file
                    if(lowest > temp) {  // Check for the best fit
                        file_arr[m] = n;
                        lowest = temp;
                    }
                }
            }
        }

        // After finding the best fit block
        fragments[m] = lowest;
        block_arr[file_arr[m]] = 1;  // Mark block as allocated
        lowest = 10000;  // Reset for the next file
    }

    // Display the result
    printf("\nFile Number\tFile Size\tBlock Number\tBlock Size\tFragment");
    for(m = 0; m < number_of_files; m++) {
        if (file_arr[m] != -1) {
            printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d", m + 1, file[m], file_arr[m] + 1, block[file_arr[m]], fragments[m]);
        }
    }
    printf("\n");

    return 0;
}
[24/09, 8:05 pm] +91 79952 47442: *Ex7(b)*
#include<stdio.h>

int main() {
    static int block_arr[10], file_arr[10];
    int fragments[10], blocks[10], files[10];
    int m, n, number_of_blocks, number_of_files, temp;

    // Input the total number of blocks
    printf("\nEnter the Total Number of Blocks:\t");
    scanf("%d", &number_of_blocks);

    // Input the total number of files
    printf("Enter the Total Number of Files:\t");
    scanf("%d", &number_of_files);

    // Input the size of the blocks
    printf("\nEnter the Size of the Blocks:\n");
    for (m = 0; m < number_of_blocks; m++) {
        printf("Block No.[%d]:\t", m + 1);
        scanf("%d", &blocks[m]);
    }

    // Input the size of the files
    printf("Enter the Size of the Files:\n");
    for (m = 0; m < number_of_files; m++) {
        printf("File No.[%d]:\t", m + 1);
        scanf("%d", &files[m]);
    }

    // Allocate files to blocks
    for (m = 0; m < number_of_files; m++) {
        for (n = 0; n < number_of_blocks; n++) {
            if (block_arr[n] != 1) {  // If block is not already allocated
                temp = blocks[n] - files[m];  // Calculate remaining space in the block

                if (temp >= 0) {  // If the block can accommodate the file
                    file_arr[m] = n;  // Assign block to file
                    fragments[m] = temp;  // Store the fragment size
                    block_arr[n] = 1;  // Mark block as allocated
                    break;
                }
            }
        }
    }

    // Print the results
    printf("\nFile Number\tBlock Number\tFile Size\tBlock Size\tFragment");
    for (m = 0; m < number_of_files; m++) {
        printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d", m + 1, file_arr[m] + 1, files[m], blocks[file_arr[m]], fragments[m]);
    }

    printf("\n");
    return 0;
}
[24/09, 8:05 pm] +91 79952 47442: *7c*
#include<stdio.h>

int main() {
    int fragments[10], blocks[10], files[10];
    int m, n, number_of_blocks, number_of_files, temp, top;
    static int block_arr[10], file_arr[10];

    // Input the total number of blocks
    printf("\nEnter the Total Number of Blocks:\t");
    scanf("%d", &number_of_blocks);

    // Input the total number of files
    printf("Enter the Total Number of Files:\t");
    scanf("%d", &number_of_files);

    // Input the size of the blocks
    printf("\nEnter the Size of the Blocks:\n");
    for (m = 0; m < number_of_blocks; m++) {
        printf("Block No.[%d]:\t", m + 1);
        scanf("%d", &blocks[m]);
    }

    // Input the size of the files
    printf("\nEnter the Size of the Files:\n");
    for (m = 0; m < number_of_files; m++) {
        printf("File No.[%d]:\t", m + 1);
        scanf("%d", &files[m]);
    }

    // Allocate files to blocks using the Worst Fit strategy
    for (m = 0; m < number_of_files; m++) {
        top = -1;  // Reset the top for each file
        for (n = 0; n < number_of_blocks; n++) {
            if (block_arr[n] != 1) {  // Check if block is free
                temp = blocks[n] - files[m];  // Calculate fragment size
                if (temp >= 0) {  // If block can fit the file
                    if (top < temp) {  // Find the largest remaining space (worst fit)
                        file_arr[m] = n;
                        top = temp;
                    }
                }
            }
        }
        if (top != -1) {  // If a suitable block was found
            fragments[m] = top;  // Store the fragment size
            block_arr[file_arr[m]] = 1;  // Mark the block as allocated
        } else {
            printf("\nFile No.[%d] of size %d could not be allocated.\n", m + 1, files[m]);
        }
    }

    // Print the results
    printf("\nFile Number\tFile Size\tBlock Number\tBlock Size\tFragment");
    for (m = 0; m < number_of_files; m++) {
        if (block_arr[file_arr[m]] == 1) {  // Only print allocated files
            printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d", m + 1, files[m], file_arr[m] + 1, blocks[file_arr[m]], fragments[m]);
        }
    }
    printf("\n");

    return 0;
}


*EX.6(1)*
#include <stdio.h>

int findLRU(int time[], int n) {
    int i, minimum = time[0], pos = 0;
    for (i = 1; i < n; ++i) {
        if (time[i] < minimum) {
            minimum = time[i];
            pos = i;
        }
    }
    return pos;
}

int main() {
    int no_of_frames, no_of_pages, frames[10], pages[30], counter = 0, time[10];
    int flag1, flag2, i, j, pos, faults = 0;

    // Input the number of frames
    printf("Enter number of frames: ");
    scanf("%d", &no_of_frames);

    // Input the number of pages
    printf("Enter number of pages: ");
    scanf("%d", &no_of_pages);

    // Input the reference string (pages)
    printf("Enter reference string: ");
    for (i = 0; i < no_of_pages; ++i) {
        scanf("%d", &pages[i]);
    }

    // Initialize all frames to -1 (indicating they are empty)
    for (i = 0; i < no_of_frames; ++i) {
        frames[i] = -1;
    }

    // Start processing each page
    for (i = 0; i < no_of_pages; ++i) {
        flag1 = flag2 = 0;

        // Check if page is already in any frame
        for (j = 0; j < no_of_frames; ++j) {
            if (frames[j] == pages[i]) {
                counter++;
                time[j] = counter;
                flag1 = flag2 = 1;
                break;
            }
        }

        // If the page is not found in frames (i.e., page fault occurs)
        if (flag1 == 0) {
            // Check for empty frame
            for (j = 0; j < no_of_frames; ++j) {
                if (frames[j] == -1) {
                    counter++;
                    faults++;
                    frames[j] = pages[i];
                    time[j] = counter;
                    flag2 = 1;
                    break;
                }
            }
        }

        // If no empty frame is available, use LRU to replace the page
        if (flag2 == 0) {
            pos = findLRU(time, no_of_frames);
            counter++;
            faults++;
            frames[pos] = pages[i];
            time[pos] = counter;
        }

        // Print the current state of frames
        printf("\n");
        for (j = 0; j < no_of_frames; ++j) {
            printf("%d\t", frames[j]);
        }
    }

    // Print the total number of page faults
    printf("\n\nTotal Page Faults = %d\n", faults);

    return 0;
}
*EX6(2) Optimal replacement algorithm*
#include <stdio.h>

int main() {
    // Variable declaration and initialization
    int frames_number, pages_number, frames[10], faults = 0, pages[30], temp[10];
    int flag1, flag2, flag3, i, j, k, pos, max, miss = 0;

    // Input the number of frames
    printf("Enter number of frames: ");
    scanf("%d", &frames_number);

    // Input the number of pages
    printf("Enter number of pages: ");
    scanf("%d", &pages_number);

    // Input the page reference string
    printf("Enter page reference string: ");
    for (i = 0; i < pages_number; ++i) {
        scanf("%d", &pages[i]);
    }

    // Initialize all frames to -1 (indicating empty frames)
    for (i = 0; i < frames_number; ++i) {
        frames[i] = -1;
    }

    // Page replacement algorithm
    for (i = 0; i < pages_number; ++i) {
        flag1 = flag2 = 0;

        // Check if the page is already in any of the frames
        for (j = 0; j < frames_number; ++j) {
            if (frames[j] == pages[i]) {
                flag1 = flag2 = 1;
                break;
            }
        }

        // If the page is not found in frames
        if (flag1 == 0) {
            for (j = 0; j < frames_number; ++j) {
                if (frames[j] == -1) {  // Empty frame found
                    faults++;
                    frames[j] = pages[i];
                    flag2 = 1;
                    break;
                }
            }
        }

        // If no empty frame is available, use Optimal Page Replacement
        if (flag2 == 0) {
            flag3 = 0;
            for (j = 0; j < frames_number; ++j) {
                temp[j] = -1;
                for (k = i + 1; k < pages_number; ++k) {
                    if (frames[j] == pages[k]) {
                        temp[j] = k;
                        break;
                    }
                }
            }

            // Find the frame that won't be used for the longest time
            for (j = 0; j < frames_number; ++j) {
                if (temp[j] == -1) {
                    pos = j;
                    flag3 = 1;
                    break;
                }
            }

            // If all frames are going to be used in the future, replace the one used last
            if (flag3 == 0) {
                max = temp[0];
                pos = 0;
                for (j = 1; j < frames_number; ++j) {
                    if (temp[j] > max) {
                        max = temp[j];
                        pos = j;
                    }
                }
            }

            frames[pos] = pages[i];  // Replace the page
            miss++;
        }

        // Print the current state of frames
        printf("\n");
        for (j = 0; j < frames_number; ++j) {
            printf("%d\t", frames[j]);
        }
    }

    // Print the total number of page misses
    printf("\n\nTotal Page Misses = %d\n", miss);

    return 0;
}*EX6(3) FIFO algorithm*
#include<stdio.h>

int main() {
    int i, j, n, a[50], frame[10], no, k, avail, count = 0;

    // Input the number of pages
    printf("\nENTER THE NUMBER OF PAGES:\n");
    scanf("%d", &n);

    // Input the page reference string
    printf("\nENTER THE PAGE NUMBERS:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    // Input the number of frames
    printf("\nENTER THE NUMBER OF FRAMES: ");
    scanf("%d", &no);

    // Initialize all frames to -1 (indicating empty frames)
    for (i = 0; i < no; i++)
        frame[i] = -1;

    j = 0;

    // Print header for the output table
    printf("\tRef String\tPage Frames\n");

    // Page replacement process
    for (i = 0; i < n; i++) {
        avail = 0;

        // Check if the page is already in any of the frames
        for (k = 0; k < no; k++) {
            if (frame[k] == a[i]) {
                avail = 1;  // Page is available (hit)
                break;
            }
        }

        // If the page is not in frames (page fault occurs)
        if (avail == 0) {
            frame[j] = a[i];  // Replace the frame using FIFO
            j = (j + 1) % no;  // FIFO replacement logic
            count++;  // Increment page fault count

            // Print the current page and frame status
            printf("%d\t\t", a[i]);
            for (k = 0; k < no; k++) {
                if (frame[k] != -1)
                    printf("%d\t", frame[k]);
                else
                    printf("-\t");
            }
            printf("\n");
        }
    }

    // Print the total number of page faults
    printf("\nTotal Page Faults = %d\n", count);

    return 0;
}

