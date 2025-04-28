```c
#include <wayland-client.h>
#include <GL/gl.h>
#include <nuklear.h>
#include <nuklear_wayland.h>

// Initialize Wayland display
struct wl_display *display = wl_display_connect(NULL);
struct wl_surface *surface = wl_compositor_create_surface(compositor);

// Nuklear context setup
struct nk_context ctx;
nk_init_default(&ctx, NULL);

// Variables for widgets
static char text_buffer[64];
static float slider_value = 0.5f;
static int checkbox_value = 0;
static int selected_item = 0;
const char *items[] = {"Option 1", "Option 2", "Option 3"};

while (running) {
    // Input handling
    nk_input_begin(&ctx);
    // Process Wayland events here
    nk_input_end(&ctx);

    // GUI layout
    if (nk_begin(&ctx, "Demo", nk_rect(50, 50, 300, 400), NK_WINDOW_BORDER)) {
        // Static Layout
        nk_layout_row_static(&ctx, 30, 100, 2);
        nk_label(&ctx, "Static Label", NK_TEXT_LEFT);
        if (nk_button_label(&ctx, "Click Me")) {
            printf("Button clicked!\n");
        }

        // Dynamic Layout
        nk_layout_row_dynamic(&ctx, 30, 2);
        nk_label(&ctx, "Dynamic Label", NK_TEXT_LEFT);
        nk_button_label(&ctx, "Dynamic Button");

        // Text Input
        nk_layout_row_dynamic(&ctx, 30, 1);
        nk_edit_string_zero_terminated(&ctx, NK_EDIT_FIELD, text_buffer, sizeof(text_buffer), nk_filter_default);

        // Slider
        nk_layout_row_dynamic(&ctx, 30, 1);
        nk_slider_float(&ctx, 0.0f, &slider_value, 1.0f, 0.1f);

        // Checkbox
        nk_layout_row_dynamic(&ctx, 30, 1);
        nk_checkbox_label(&ctx, "Enable Feature", &checkbox_value);

        // Combobox
        nk_layout_row_dynamic(&ctx, 30, 1);
        selected_item = nk_combo(&ctx, items, 3, selected_item, 30, nk_vec2(200, 200));
    }
    nk_end(&ctx);

    // Render UI
    nk_wayland_render(surface, &ctx);
}

// Cleanup
nk_free(&ctx);
wl_display_disconnect(display);

```
