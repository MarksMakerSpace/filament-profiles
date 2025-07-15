# Filament Data Submission Guide for Manufacturers

This guide is designed for product managers from filament manufacturers to help you understand the data we need for integration. By providing this data, you enable us to accurately represent your products in our system and ensure a seamless experience for customers.

## Why Your Data Matters

Providing detailed and accurate data about your filament products allows us to:
- Display your products with the correct specifications and images.
- Ensure customers can find your products easily.
- Provide accurate pricing and availability information.
- Enable optimal printing parameters for your filaments.

## Data We Need

Below is a list of the data fields we require, along with descriptions and examples to help you map your inventory system data to our schema.

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

## Mapping Your Data

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

## Submitting Your Data

You can submit your data in structured formats like CSV or Excel. Ensure the column names match the mapping provided above. If you have additional fields not listed here, feel free to include them, and we will review their relevance.

## Need Help?

If you have any questions or need assistance with mapping your data, please contact us at [support@3dfilamentprofiles.com](mailto:support@3dfilamentprofiles.com). We're here to help!