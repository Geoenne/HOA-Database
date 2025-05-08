# HOA-Database
A database management system using SQL and Python for a large HOA 
INSERT INTO Buildings (name, address, city, state, total_units, year_built, amenities)
VALUES
    ('Southwyck', ‘1 Carriage Drive', ‘Scotch Plains', 'NJ', 10, 1980, 'Pool, Clubhouse, Roadways, Bridge’),
    ('Maple Residences', '456 Maple Ave', 'San Francisco', 'CA', 15, 2010, 'Gym, Parking Garage'),
    ('Oak Apartments', '789 Oak St', 'Portland', 'OR', 8, 2000, 'Outdoor Patio');
INSERT INTO Units (building_id, unit_number, floor, type, occupancy_status, owner_id, monthly_rent)
VALUES
    (1, '101', 1, '1-bedroom', 'occupied', 1, 1500.00),
    (1, '102', 1, 'studio', 'vacant', NULL, 1200.00),
    (1, '201', 2, '2-bedroom', 'occupied', 2, 1800.00),
    (2, '101', 1, 'studio', 'occupied', 3, 1300.00),
    (2, '102', 1, '1-bedroom', 'vacant', NULL, 1600.00),
    (3, '201', 2, '1-bedroom', 'occupied', 4, 1400.00),
    (3, '301', 3, '2-bedroom', 'occupied', 5, 2000.00);
INSERT INTO UnitGroups (building_id, group_name, description)
VALUES
    (1, 'First Floor', 'All units on the first floor of Sunset Towers'),
    (1, 'Second Floor', 'All units on the second floor of Sunset Towers'),
    (2, 'First Floor', 'All units on the first floor of Maple Residences'),
    (3, 'Premium Units', 'Top floor units in Oak Apartments');
INSERT INTO UnitGroupMemberships (unit_id, group_id)
VALUES
    (1, 1),  -- Unit 101 in Southwyck is in the "First Floor" group
    (2, 1),  -- Unit 102 in Southwyck is in the "First Floor" group
    (3, 2),  -- Unit 201 in Southwyck  is in the "Second Floor" group
    (4, 3),  -- Unit 101 in Maple Residences is in the "First Floor" group
    (6, 4),  -- Unit 201 in Oak Apartments is in the "Premium Units" group
    (7, 4);  -- Unit 301 in Oak Apartments is in the "Premium Units" group
SELECT u.unit_number, u.type, u.occupancy_status
FROM Units u
JOIN Buildings b ON u.building_id = b.building_id
WHERE b.name = 'Sunset Towers';
SELECT u.unit_number, b.name AS building_name
FROM Units u
JOIN UnitGroupMemberships ugm ON u.unit_id = ugm.unit_id
JOIN UnitGroups g ON ugm.group_id = g.group_id
JOIN Buildings b ON u.building_id = b.building_id
WHERE g.group_name = 'First Floor';
SELECT u.unit_number, u.floor, u.monthly_rent
FROM Units u
JOIN UnitGroupMemberships ugm ON u.unit_id = ugm.unit_id
JOIN UnitGroups g ON ugm.group_id = g.group_id
JOIN Buildings b ON u.building_id = b.building_id
WHERE b.name = 'Oak Apartments' AND g.group_name = 'Premium Units';
