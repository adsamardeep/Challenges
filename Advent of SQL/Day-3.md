-- Drop the table if it exists
DROP TABLE IF EXISTS christmas_menus CASCADE;

-- Create the table
CREATE TABLE christmas_menus (
  id SERIAL PRIMARY KEY,
  menu_data TEXT
);

-- Insert sample data
INSERT INTO christmas_menus (id, menu_data) VALUES
(1, '<menu version="1.0">
    <dishes>
        <dish>
            <food_item_id>99</food_item_id>
        </dish>
        <dish>
            <food_item_id>102</food_item_id>
        </dish>
    </dishes>
    <total_count>80</total_count>
</menu>');

-- Main query to find the most frequent dish
WITH CombinedData AS (
    SELECT id,
           ExtractValue(menu_data, '/menu/total_count') AS total_count,
           ExtractValue(menu_data, '/menu/dishes/dish/food_item_id') AS food_item_id,
           ExtractValue(menu_data, '/menu/@version') AS schema_version
    FROM christmas_menus
    UNION ALL
    SELECT id,
           ExtractValue(menu_data, '/menu/totalCount') AS total_count,
           ExtractValue(menu_data, '/menu/dishes/dish/foodItemId') AS food_item_id,
           ExtractValue(menu_data, '/menu/@version') AS schema_version
    FROM christmas_menus
),
FilteredData AS (
    SELECT food_item_id
    FROM CombinedData
    WHERE total_count > 78
)
SELECT food_item_id, COUNT(*) AS frequency
FROM FilteredData
GROUP BY food_item_id
ORDER BY frequency DESC
LIMIT 1;
