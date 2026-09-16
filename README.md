# SABOR — Interactive 3D / AR Menu

A single `index.html` with inline CSS and JavaScript. No frameworks, npm, or build step. Internet access is required for the model-viewer CDN and sample models.

## Deploy with GitHub Pages

1. Create a public GitHub repository (or use an existing Pages-compatible repository).
2. Upload `index.html` and this `README.md` to the root of `main`.
3. Open **Settings → Pages → Build and deployment**.
4. Select **Deploy from a branch**, choose **main** and **/(root)**, then **Save**.
5. Wait for deployment and open the HTTPS URL shown in Pages settings, typically `https://USERNAME.github.io/REPOSITORY/`.

No workflow or package installation is required. Future commits to the publishing branch update the site. [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Add real food models

Create a `models` directory beside `index.html` and upload your scans. Example:

```text
index.html
README.md
models/burger.glb
models/burger.usdz
```

Find the burger entry in the `dishes` array and replace these fields:

```js
glb: "./models/burger.glb",
usdz: "./models/burger.usdz",
demo: false
```

Repeat for the other five dishes. Each entry includes its suggested filenames in a comment. All six use the official astronaut sample initially; no food scans are included.

- GLB powers the inline 3D preview and Android Scene Viewer.
- USDZ powers iOS Quick Look. Use the same scan, orientation and scale in both formats.
- If you do not have USDZ, set `usdz: ""`; model-viewer can generate it for Quick Look. Test the conversion on an iPhone.
- Use relative paths beginning with `./models/`, respecting filename case. Leading `/models/` paths break on many GitHub project sites.
- Export GLB with embedded textures, correct physical dimensions in metres, and its base at ground level. Aim for a few MB per dish for mobile loading.
- After replacing every sample, update the demo notice and remove the sample attribution if no sample assets remain.
- Edit restaurant branding in the header, colours in `:root`, and dish names, prices, descriptions and tags in `dishes`.

[Official model-viewer AR documentation](https://modelviewer.dev/examples/augmentedreality/).

## Generate the QR code

1. Copy your final deployed **HTTPS page URL**, including the repository path. Do not use a GitHub source-file URL.
2. Paste it into a QR-code generator's URL field and choose a static QR code.
3. Export SVG for printing or a high-resolution PNG for digital sharing.
4. Keep a clear white margin around a dark code. Scan the exported/printed code on both iPhone and Android before sharing.

The QR code remains valid when you update dishes, provided the page URL stays the same.

## Mobile behaviour and checks

- Category tabs scroll to sections; tapping a dish opens one inline 3D viewer at a time.
- Drag to rotate, pinch to zoom, and scroll vertically through the menu.
- The native **View in AR** button appears on supported devices. iOS uses Quick Look; Android uses Scene Viewer. Unsupported devices retain the 3D preview and receive guidance.
- Open the deployed HTTPS page directly in Safari on iPhone or Chrome on an AR-capable Android device. Some embedded social-app browsers cannot launch AR; use **Open in browser**.
- Camera/AR permissions are handled by the native viewer. A QR scan alone does not start the camera.
- AR depends on device support and native AR services; confirm placement on real phones. Desktop 3D success does not verify mobile AR.
- Loading errors show a retry option. Reduced-motion settings disable automatic rotation.
- For local 3D development, serve the folder with `python -m http.server 8000` and visit `http://localhost:8000`. Use the deployed HTTPS URL for phone AR tests.

## Assumptions

SABOR is placeholder branding; prices are AED; dietary labels are sample content. This is a browsing menu, with no ordering or payment backend. Astronaut stand-ins do not represent food appearance or serving size. Native AR placement must be verified on your target phones.