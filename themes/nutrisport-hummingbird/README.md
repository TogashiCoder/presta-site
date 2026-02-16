# NutriSport Hummingbird Child Theme

Child theme of Hummingbird for PrestaShop. Used for Task 10 (theme customization).

## Contents

- **config/theme.yml** – parent theme, name, assets (custom.css)
- **assets/css/custom.css** – custom styles (e.g. Info livraison block)
- **templates/catalog/_partials/product-additional-info.tpl** – adds "Info livraison" block on product page
- **templates/catalog/_partials/product-prices.tpl** – override with wrapper (2nd .tpl)

## Activation

1. Copy this folder into PrestaShop `themes/` (e.g. via Docker volume mount or `docker cp`).
2. In Back Office: Design > Theme & Logo, select "NutriSport Hummingbird Child" and save.
3. Clear cache if needed.

## Preview image

If the theme does not show a preview in BO, copy `preview.png` from the parent theme (Hummingbird) in `themes/hummingbird/` into this folder.
