-- Settings defaultRadius = 50 ESPEnabled = true

-- Placeholder for detecting players/objects function isTeamMate(player) -- Replace with actual team check logic return player.team == "YourTeamName" end

function getPlayersInRadius(radius) -- Replace with actual player fetching logic local players = {} -- List of players detected within radius for _, player in ipairs(getAllPlayers()) do if player.distance <= radius and not isTeamMate(player) then table.insert(players, player) end end return players end

-- Draw ESP Boxes function drawESP() if not ESPEnabled then return end

local players = getPlayersInRadius(defaultRadius)
for _, player in ipairs(players) do
    drawBox(player.position, "red") -- Replace with actual drawing function
end

end

-- UI Elements function createUI() local ui = createWindow("ESP Controls") -- Replace with actual UI creation library

local radiusSlider = createSlider(ui, "Radius", 10, 100, defaultRadius, function(value)
    defaultRadius = value
end)

local enableToggle = createToggle(ui, "Enable ESP", ESPEnabled, function(value)
    ESPEnabled = value
end)

showWindow(ui)

end

-- Main Loop function main() createUI()

while true do
    drawESP()
    wait(0.1) -- Adjust loop interval for performance
end

end

-- Start the script main()

