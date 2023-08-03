/**
 * Custom price format for WooCommerce regular price in lakhs and crores.
 */
function custom_wc_price_format($price, $product) {
    if ($product->is_type('variable')) {
        // Get the minimum and maximum regular prices of the variations
        $variation_prices = $product->get_variation_prices('regular');
        $min_regular_price = min($variation_prices['price']);
        $max_regular_price = max($variation_prices['price']);

        // Convert the minimum and maximum prices to lakhs or crores format
        $formatted_min_price = format_price($min_regular_price);
        $formatted_max_price = format_price($max_regular_price);

        // Display the price range
        $formatted_price = $formatted_min_price . ' - ' . $formatted_max_price;
    } else {
        $regular_price = $product->get_regular_price();

        // Check if the regular price is set and not empty
        if (!empty($regular_price)) {
            $formatted_price = format_price($regular_price);
        } else {
            $formatted_price = '';
        }
    }

    return $formatted_price;
}
add_filter('woocommerce_get_price_html', 'custom_wc_price_format', 10, 2);

/**
 * Helper function to format the price in lakhs or crores with ₹ symbol.
 */
function format_price($price) {
    $price = floatval($price);
    $formatted_price = '';

    // Convert price to crore if it's greater than or equal to 1,00,00,000
    if ($price >= 10000000) {
        $price = $price / 10000000;
        $formatted_price = '₹ ' . number_format($price, 2) . ' Cr*';
    }
    // Convert price to lakh if it's greater than or equal to 1,00,000
    elseif ($price >= 100000) {
        $price = $price / 100000;
        $formatted_price = '₹ ' . number_format($price, 2) . ' Lakh*';
    } else {
        $formatted_price = '₹ ' . number_format($price, 2);
    }

    return $formatted_price;
}
