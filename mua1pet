repeat task.wait() until game:IsLoaded()

local RS = game:GetService("ReplicatedStorage")
local API = RS:WaitForChild("API")
local ClientData = require(RS.ClientModules.Core.ClientData)

local TARGET_EGG_KIND = "endangered_2026_endangered_egg"

local function countPets()
    local inventory = ClientData.get("inventory")
    local pets = (inventory and inventory.pets) or {}
    local total = 0
    for _, _ in pairs(pets) do
        total = total + 1
    end
    return total
end

local function tryBuyEgg()
    local buyCalls = {
        function()
            return API:WaitForChild("ShopAPI/BuyItem", 5):InvokeServer(TARGET_EGG_KIND, 1)
        end,
        function()
            return API:WaitForChild("ShopAPI/BuyItem", 5):InvokeServer(TARGET_EGG_KIND)
        end,
        function()
            return API:WaitForChild("ShopAPI/BuyItemWithCurrency", 5):InvokeServer(TARGET_EGG_KIND, 1)
        end
    }

    for _, fn in ipairs(buyCalls) do
        local ok, result = pcall(fn)
        if ok then
            return true, result
        end
    end
    return false, nil
end

local petCount = countPets()
print("[1pet] So luong pet hien tai:", petCount)

if petCount <= 1 then
    local ok = tryBuyEgg()
    if ok then
        print("[1pet] Da mua them:", TARGET_EGG_KIND)
    else
        warn("[1pet] Mua trung that bai. Kiem tra lai remote mua vat pham.")
    end
else
    print("[1pet] Da du pet, khong can mua them.")
end
