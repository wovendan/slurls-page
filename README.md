🧭 Why This Page Uses Conditional SLURLs
Purpose:
This HTML page detects whether it is being displayed inside the Second Life viewer or a regular web browser. Based on that, it serves SLURLs in the format that will actually work for the user’s environment.

✅ Problem
In web browsers, only http://maps.secondlife.com/... links will open Firestorm or the SL viewer (if installed).

Inside Second Life, only secondlife:///app/teleport/... links actually trigger a teleport when clicked on an in-world prim with media-on-a-prim.

Using the wrong type of link causes nothing to happen—or shows a security warning like “SLurl received from an untrusted browser.”

✅ Solution
We use JavaScript to detect whether the viewer is Second Life (by checking the navigator.userAgent string). Then we dynamically create each link in the appropriate format:

js
Copy
Edit
isSL ? "secondlife:///app/teleport/..." : "https://maps.secondlife.com/..."
This ensures that the same web page works in both environments without needing to maintain two versions.

🔄 How to Adapt This for Images
If you want to include clickable images instead of text links, just replace this part:

js
Copy
Edit
const a = document.createElement("a");
a.href = isSL ? inworldSLURL : webSLURL;
a.target = isSL ? "_self" : "_blank";
a.textContent = loc.name;
with something like this:

js
Copy
Edit
const img = document.createElement("img");
img.src = `images/${loc.name.replace(/\s+/g, "_")}.jpg`; // e.g., "To_Kill_a_Mockingbird.jpg"
img.alt = loc.name;
img.style = "width: 200px; display: block; margin-bottom: 1em;";

const a = document.createElement("a");
a.href = isSL ? inworldSLURL : webSLURL;
a.target = isSL ? "_self" : "_blank";
a.appendChild(img);

linkArea.appendChild(a);
Just make sure your images (e.g. images/To_Kill_a_Mockingbird.jpg) are uploaded to the correct path in your GitHub repo.
