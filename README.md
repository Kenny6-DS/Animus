# Developer's Notes:
The following is a suggested component level structure and options for potential build process. 
We could, in theory, leverage Astro's build process with configuration if we wanted to make this a seamless transition. 
Alternatively, we could use Parcel as our bundler, which is not uncommon for component-level builds. The only outstanding question is how seamless do we want to make this between 
"sandboxing" our modules, components, and subcomponents -- and subsequently making them available for use in Umbraco templates. 

## Configuration
- Launch Configuration handled in package.json
- Tailwind Configuration in tailwind.config.js

## Workflow
1. Develop components in Astro environment
2. Test with `astro dev`
3. Bundle (using either Astro or Parcel)
4. Copy dist folder to Umbraco (or simply copy primary component file contents into a separate razor file, complete with asset import urls)
5. Reference in Razor templates

## Build Option Comparisons

### Astro Build
- Uses built-in bundling
- Handles TypeScript and JSX
- Component-level output requires configuration

### Parcel Build
- Zero-config bundling
- Component-level processing
- Handles Tailwind per component
- Self-contained bundles per component
  

## Development Process
### 1. Development (Astro)
```
src/components/MyComponent/
├── index.astro        # Main component file & exports
├── styles.css         # Component-specific styles
├── scripts.ts         # Client-side logic
├── types.ts          # TypeScript interfaces/types
├── assets/           # Component-specific assets
│   ├── images/
│   └── icons/
└── subcomponents/    # Child components used only by this component
    ├── SubCompA.astro
    └── SubCompB.astro
```

### 2. Build Output
With either Astro's build process or Parcel:
```
dist/components/MyComponent/
├── index.js          # Bundled JS
├── styles.css        # Processed CSS with Tailwind
└── assets/          # Optimized assets
```

### 3. Umbraco Integration
```razor
@* _Layout.cshtml or component template *@
<script src="~/dist/components/MyComponent/index.js"></script>
<link rel="stylesheet" href="~/dist/components/MyComponent/styles.css">
<div id="my-component-mount"></div>
```


## Useful Links
- [Astro Getting Started](https://docs.astro.build/en/getting-started/)
- [Astro Components](https://docs.astro.build/en/basics/astro-components/)
- [Parcel Documentation](https://parceljs.org/docs/)
