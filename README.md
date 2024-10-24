live view : https://newgithubuser709.github.io/Gallery-hover/

```hash
// Function to detect mouse enter/leave direction
function getMouseDirection(e, element) {
    const rect = element.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    const w = rect.width;
    const h = rect.height;

    const top = Math.abs(y);
    const bottom = Math.abs(h - y);
    const left = Math.abs(x);
    const right = Math.abs(w - x);

    const min = Math.min(top, bottom, left, right);

    if (min === top) return "top";
    if (min === bottom) return "bottom";
    if (min === left) return "left";
    if (min === right) return "right";
}

// Add event listeners to each box
document.querySelectorAll(".box").forEach((box) => {
    const overlay = box.querySelector(".overlay");

    box.addEventListener("mouseenter", (e) => {
        const direction = getMouseDirection(e, box);

        // Disable transitions for immediate reset
        overlay.style.transition = "none";

        // Instantly reset the overlay's position based on entry direction
        switch (direction) {
            case "top":
                overlay.style.transform = "translateY(-100%)";
                break;
            case "bottom":
                overlay.style.transform = "translateY(100%)";
                break;
            case "left":
                overlay.style.transform = "translateX(-100%)";
                break;
            case "right":
                overlay.style.transform = "translateX(100%)";
                break;
        }

        // Small timeout to ensure instant reset before sliding in
        setTimeout(() => {
            overlay.style.transition = "transform 0.3s ease"; // Re-enable transition for smooth sliding
            overlay.style.transform = "translate(0, 0)"; // Smoothly slide into view from the new direction
        }, 0); // Slight delay to apply the change
    });

    box.addEventListener("mouseleave", (e) => {
        const direction = getMouseDirection(e, box);

        // Smoothly slide out in the direction of mouse exit
        overlay.style.transition = "transform 0.3s ease"; // Ensure smooth transition
        switch (direction) {
            case "top":
                overlay.style.transform = "translateY(-100%)";
                break;
            case "bottom":
                overlay.style.transform = "translateY(100%)";
                break;
            case "left":
                overlay.style.transform = "translateX(-100%)";
                break;
            case "right":
                overlay.style.transform = "translateX(100%)";
                break;
        }
    });
});
```
