```c
#include <wayland-client.h>
#include <nuklear.h>
#include <nuklear_wayland.h>
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <string.h>

// File list variables
#define MAX_FILES 256
char *file_list[MAX_FILES];
int file_count = 0;
int selected_index = 0;

// Function to load files from a directory
void load_files(const char *path) {
    struct dirent *entry;
    DIR *dir = opendir(path);
    if (!dir) return;

    file_count = 0;
    while ((entry = readdir(dir)) && file_count < MAX_FILES) {
        file_list[file_count] = strdup(entry->d_name);
        file_count++;
    }
    closedir(dir);
}

// Handle keyboard input (Wayland key events)
void handle_input(struct wl_keyboard *keyboard, uint32_t key) {
    if (key == 103 && selected_index > 0) selected_index--; // Key Up
    if (key == 108 && selected_index < file_count - 1) selected_index++; // Key Down
}

// Nuklear UI setup
struct nk_context ctx;
nk_init_default(&ctx, NULL);

if (nk_begin(&ctx, "File Manager", nk_rect(50, 50, 300, 400), NK_WINDOW_BORDER)) {
    nk_layout_row_dynamic(&ctx, 30, 1);

    // File list with highlight bar
    for (int i = 0; i < file_count; i++) {
        if (i == selected_index) {
            nk_style_push_color(&ctx, &ctx.style.button.normal.data.color, nk_rgb(100, 100, 255));
        }
        if (nk_button_label(&ctx, file_list[i])) {
            printf("Selected: %s\n", file_list[i]);
        }
        if (i == selected_index) {
            nk_style_pop_color(&ctx);
        }
    }
}
nk_end(&ctx);

// Cleanup
for (int i = 0; i < file_count; i++) free(file_list[i]);
nk_free(&ctx);

```
