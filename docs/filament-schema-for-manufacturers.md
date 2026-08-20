# Filament Data Submission Guide for Manufacturers

This guide is for filament manufacturers who want their products accurately represented on [3D Filament Profiles](https://3dfilamentprofiles.com). It covers the three ways to get your catalog into our database — from fully automated (recommended) to a one-time spreadsheet.

Accurate manufacturer data lets us:

- Display your products with the correct names, colors, and specifications.
- Show your product pages and images instead of user-submitted approximations.
- Keep your catalog current automatically — new colors appear the day you launch them.
- Provide optimal printing parameters for your filaments.

If you're going to the trouble of submitting data, also look at our **[Brand Partner Program](https://3dfilamentprofiles.com/partners)** — the free tier gives your team direct, curated control of your listings, a content slot on your brand page, and automatic price/sale tracking from your store.

## Option 1 — You sell on Shopify: nothing to build

If your store runs on Shopify, we can almost certainly ingest it as-is. Our scraper reads the public `/products.json` catalog that every open Shopify storefront exposes, and re-syncs it daily. This is how we ingest Polymaker, ELEGOO, SUNLU, and a dozen other brands.

Email [support@3dfilamentprofiles.com](mailto:support@3dfilamentprofiles.com) with your storefront URL (and the currency/region of each storefront if you run several) and we'll take it from there.

To get the best results from your existing product data:

- Give products a `product_type` of "Filament" (or a `filament` tag) so we can tell filament from printers and accessories.
- Name your variant options **Color**, **Diameter**, and **Weight** — we resolve them by option *name*, not position.
- Fill in variant `barcode` with the GTIN/UPC where you have it — it's our highest-confidence way to match your products to entries users have already created.

## Option 2 — No Shopify store: host a product feed on your own site

If your site isn't a store (or isn't on Shopify), you can publish a single JSON document on your own domain — e.g. `https://www.example.com/products.json` — in Shopify's `products.json` format, and we ingest it exactly the same way, re-checking daily. A static file containing your entire catalog is fine; if you later open a Shopify store, nothing changes on our side.

### Feed format

```json
{
  "products": [
    {
      "id": 101,
      "title": "PLA Basic",
      "handle": "pla-basic",
      "product_type": "Filament",
      "vendor": "ExampleCo",
      "tags": "filament, PLA",
      "body_html": "<p>Optional product description.</p>",
      "options": [
        { "name": "Color", "position": 1 },
        { "name": "Diameter", "position": 2 },
        { "name": "Weight", "position": 3 }
      ],
      "variants": [
        {
          "id": 1001,
          "title": "White / 1.75mm / 1kg",
          "option1": "White",
          "option2": "1.75mm",
          "option3": "1kg",
          "sku": "EX-PLA-WH-175",
          "barcode": "123456789012",
          "price": "19.99",
          "available": true,
          "grams": 1000
        }
      ],
      "images": [
        { "id": 1, "src": "https://www.example.com/images/pla-basic-white.jpg", "variant_ids": [1001] }
      ]
    }
  ]
}
```

One `product` per product family (PLA Basic, PLA Matte, PETG…), one `variant` per color/diameter/weight combination.

### Field notes

| Field | Notes |
| --- | --- |
| `title` | Product family name. Avoid "sample", "swatch", "bundle" in filament titles — those patterns are auto-excluded. |
| `handle` | URL slug. We link users to `<your-domain>/products/<handle>` — make sure that URL exists (or tell us your URL pattern). |
| `product_type` / `tags` | At least one of these should identify the product as filament. |
| `options[].name` | We recognize **Color** (also Colour/Farbe), **Diameter**/Size (values must contain "mm", e.g. "1.75mm"), **Weight** (also Net Weight/Gewicht). Each option needs its `position` (1–3) matching the variant's `option1`–`option3`. |
| `variants[].id` | Any unique number, but keep it **stable across feed updates** — it's how we track a variant over time. Don't renumber. |
| `variants[].sku` | Your internal SKU. Used for matching and display. |
| `variants[].barcode` | GTIN/UPC (12–14 digits). The strongest matching signal we have — fill it in if you possibly can. |
| `variants[].price` | Optional. Decimal string in a single, consistent currency — tell us which one. Omit if you don't sell retail yet. |
| `variants[].available` | Stock status; lets us show availability. |
| `images[]` | Optional. `variant_ids` maps an image to specific variants (e.g. a per-color photo). |

Email us the feed URL once it's live and we'll add you to the daily sync.

## Option 3 — One-time spreadsheet submission

If a feed isn't practical yet, we accept a CSV or Excel workbook for a one-time import. Be aware it goes stale the moment you launch a new color — we'd encourage pairing it with Option 1 or 2 for ongoing updates.

Below are the fields we can ingest, along with descriptions and examples to help you map your inventory system's columns to our schema.

### Required Fields

| Field Name      | Description                                                                           | Example                                   |
| --------------- | ------------------------------------------------------------------------------------- | ----------------------------------------- |
| `brand`         | The name of your brand (see [our Brands page](https://3dfilamentprofiles.com/brands)) | "FilamentCo"                              |
| `material`      | The material of the filament*                                                         | "PLA", "ABS", "PETG"                      |
| `material_type` | The type of material (e.g., specialty or subcategory)*                                | "Silk", "CF",                             |
| `color`         | The color of the filament                                                             | "Red", "Blue", "Magenta / Purple"         |
| `rgb`           | The RGB color code for the filament                                                   | "#FF0000"                                 |
| `image`         | A URL to an image of the filament                                                     | "https://example.com/images/filament.jpg" |
| `website`       | A URL to the product page on your website                                             | "https://example.com/products/filament"   |
| `price_data`    | The current price of the filament                                                     | "19.99"                                   |
| `currency`      | The currency of the price                                                             | "USD", "EUR"                              |
| `sku`           | Manufacturer SKU for the filament                                                     | "PLA-RED-1KG"                             |
| `upc`           | GTIN/UPC code for the filament                                                        | "123456789012"                            |

\* _The `material` and `material_type` fields are essential for categorizing your filament products accurately. Please ensure they are filled out correctly. The list of options can be found on our [Materials Page](https://3dfilamentprofiles.com/materials)._

_Don't have some of these yet (per-product URLs, images, prices, UPCs)? Send what you have — names, materials, SKUs, and colors are enough to start, and the rest can be supplemented later._

### Optional Fields

#### Additional Product Information

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `upc_refill`           | GTIN/UPC code for refills                      | "123456789013"                               |                                |
| `datasheet_url`        | URL to technical datasheet                     | "https://example.com/datasheet.pdf"          |                                |

#### Temperature Settings

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `temp_min`             | Minimum nozzle temperature                     | "190"                                        | °C                             |
| `temp_max`             | Maximum nozzle temperature                     | "220"                                        | °C                             |
| `bed_temp_min`         | Minimum bed temperature                        | "60"                                         | °C                             |
| `bed_temp_max`         | Maximum bed temperature                        | "80"                                         | °C                             |
| `chamber_temp`         | Recommended chamber temperature                | "40"                                         | °C                             |
| `softening_temp`       | Softening temperature                          | "60"                                         | °C                             |

#### Drying Parameters

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `dry_temp_max`         | Maximum drying temperature                     | "45"                                         | °C                             |
| `dry_time`             | Recommended drying time                        | "4"                                          | hours (max 24)                |

#### Physical Properties

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `density`              | Filament density                               | "1240"                                       | mg/cm³ (e.g., 1240 = 1.24g/cm³) |
| `diameter`             | Filament diameter                              | "1750"                                       | µm (1750 or 2850)             |
| `nominal_weight`       | Nominal weight of the spool                    | "1000"                                       | grams                          |
| `spool_weight`         | Weight of the empty spool                      | "150"                                        | grams                          |
| `shrinkage`            | Material shrinkage percentage                  | "0.5"                                        | percentage (0-100)             |

#### Print Settings

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `fan_speed_min`        | Minimum fan speed percentage                   | "50"                                         | percentage (0-100)             |
| `fan_speed_max`        | Maximum fan speed percentage                   | "100"                                        | percentage (0-100)             |
| `flow_ratio`           | Flow ratio adjustment                          | "1.05"                                       | multiplier                     |
| `max_volumetric_speed` | Maximum volumetric speed                       | "15"                                         | mm³/s                          |
| `k_value`              | K-value for the filament                       | "0.02"                                       |                                |

#### Advanced Settings

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `ironing_speed`        | Recommended ironing speed                      | "15"                                         | mm/s                           |
| `ironing_flow`         | Ironing flow percentage                        | "10"                                         | percentage (0-100)             |
| `glue`                 | Glue requirement indicator                     | "1"                                          | 0=none, 1=recommended, 2=required |

#### Compatibility

| Field Name             | Description                                    | Example                                      | Units/Notes                    |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- | ------------------------------ |
| `ams`                  | Compatible AMS types                           | "ams,ams-lite"                               | Comma-separated: ams, ams-lite, ams-2-pro, ams-ht, mmu |
| `build_plate`          | Compatible build plate types                   | "pei,textured-pei"                           | Comma-separated: pei, textured-pei, cool, engineering, superTack, cryrogrip, g10, cf, glueMaybe, glueNeeded |
| `adapter_url`          | URL for adapter information                    | "https://example.com/adapter-info"           |                                |

### AMS Options

When specifying AMS compatibility, use these values:
- `ams`: AMS
- `ams-lite`: AMSLite  
- `ams-2-pro`: AMS 2 Pro
- `ams-ht`: AMS HT
- `mmu`: MMU

### Build Plate Options

When specifying build plate compatibility, use these values:
- `pei`: Smooth PEI
- `textured-pei`: Textured PEI
- `cool`: Cool Plate
- `engineering`: Engineering Plate
- `superTack`: SuperTack Cool Plate
- `cryrogrip`: CryroGrip
- `g10`: G10
- `cf`: Carbon Fiber
- `glueMaybe`: Glue Recommended
- `glueNeeded`: Glue Required

### Mapping Your Data

Here's how you can map your inventory system data to our schema:

| Your Column Name       | Our Field Name            | Notes                                |
| ---------------------- | ------------------------- | ------------------------------------ |
| SKU                    | `sku`                     | Provide the SKU for each product     |
| Manufacturer           | `brand`                   | Use your brand name                  |
| Category               | `material`                | Specify the material category        |
| Product Type           | `material_type`           | Specify the type of material         |
| Product Name           | `color`                   | Color                                |
| RGB Color              | `rgb`                     | Provide the RGB color code           |
| Product URL            | `website`                 | Provide the URL to the product page  |
| Image URL              | `image`                   | Provide the URL to the product image |
| Product Description    | `product_description`     | Provide a detailed description       |
| Current Price          | `manufacturer_price_Data` | Provide the current price            |
| Currency               | `currency`                | Provide the currency of the price    |
| Print Temperature      | `temp_min`, `temp_max`    | Nozzle temperature range             |
| Bed Temperature        | `bed_temp_min`, `bed_temp_max` | Heated bed temperature range    |
| Filament Density       | `density`                 | In mg/cm³                            |
| Spool Weight           | `nominal_weight`          | Total weight including filament      |
| Empty Spool Weight     | `spool_weight`            | Weight of empty spool only           |

Note that the temperature, drying, physical, and print-setting fields above are welcome alongside **any** submission path — a feed (Options 1–2) covers the catalog itself, and a one-time spreadsheet of technical specs per product line is a great supplement to it.

## Submitting Your Data

- **Feed (Options 1–2):** email your storefront or feed URL to [support@3dfilamentprofiles.com](mailto:support@3dfilamentprofiles.com).
- **Spreadsheet (Option 3):** email the CSV/Excel file to the same address, with column names matching the mapping above. Extra columns are fine — we'll review their relevance.

## Need Help?

If you have any questions or need assistance with mapping your data, please contact us at [support@3dfilamentprofiles.com](mailto:support@3dfilamentprofiles.com). We're here to help!
