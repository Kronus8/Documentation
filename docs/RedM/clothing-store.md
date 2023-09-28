# :necktie: Clothing Store
Documentation relating to the kd_clothingstore.

:::tabs
== BUY
[Buy the script](https://store.kaddarem.com/package/5526960)
== PREVIEW
<iframe width="560" height="315" src="https://www.youtube.com/embed/afp8_zY7WX0?si=tWRzRmBMctwgdtKA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
:::

## 1. Installation
kd_clothingstore works with VORP & RedEM:RP (2023 & old) frameworks. 

To install kd_clothingstore:
- Drag and drop the resource into your resources folder
  - kd_clothingstore 
- Add this ensure in your server.cfg
  - `ensure kd_clothingstore`
- Be sure you remove your previous clothing store script

::: details For RedEM:RP (old only)
You have to edit the keep the ensure of redemrp_clothing and replace it with this empty resource :

https://github.com/kaddarem-tebex/redemrp_clothing/releases
:::

⚠ If you want to use clothes as items. You have to create some items. The list of items is in Config.clothesItem variable in the config file. ⚠

Congratulation, the **Clothing Store** script is ready to be used!

## 2. Usage
Go on the store (blip on the map) to get the prompt. Press the key to open the menu.

## 3. Config.lua

:::details Config.lua
```lua
Config = {}

Config.Debug = false
Config.BlipSprite = `blip_shop_tailor`	 -- Clothing shop sprite
Config.BlipSpriteWardrobes = `blip_shop_wardrobe`
Config.DisplayOutfitId = false
Config.PercentResell = 0.33 -- Use 0 tu turn off the resell feature : 0.5 = 50% of the initial price
Config.OpenStoreNewCharacter = true
Config.EnablePrompt = true
Config.ExtraLightIntensity = 10.0 -- Light added in the store to see better the character
Config.OffsetRoutingBucket = 0 --value added to the serverID of the player to define the instance ID
Config.enableClothesManagement = true --use false to turn off the clothes management feature

Config.commands = { --set false to disable a command
	refreshAllClothes = "rac" --command to refresh all clothes, use "/rac 0" to only update clothes states
}

Config.oldVORPChar = false --(Only for VORP users) to use the C# version of VORP Character

Config.Keys = {
	enter = "INPUT_FRONTEND_RB",
	buyGold = "INPUT_INTERACT_ANIMAL",
	turn = "INPUT_CONTEXT_X",
	delete = "INPUT_SWITCH_SHOULDER",
	resell = "INPUT_LOOK_BEHIND"
}

Config.KeysDisabled = {
	`INPUT_MOVE_UD`,
	`INPUT_MOVE_LR`,
	`INPUT_MOVE_LB`,
	`INPUT_COVER`
}

Config.clothesInItem = true -- set false to disable this feature
Config.clothesItem = { -- Only necessary if Config.clothesInItem = true
	gloves = 'gloves',
	eyewear = 'eyewear',
  dresses = 'dresses',
	shirts_full = 'shirts_full',
  armor = 'armor',
	gauntlets = 'gauntlets',
	suspenders = 'suspenders',
	neckties = 'neckties',
	neckwear = 'neckwear',
	vests = 'vests',
	coats = 'coats',
	coats_closed = 'coats',
	cloaks = 'cloaks',
	ponchos = 'ponchos',
	masks = 'masks',
	masks_large = 'masks',
	hats = 'hats',
	accessories = 'accessories',
	loadouts = 'loadouts',
	satchels = 'satchels',
	jewelry_rings_right = 'jewelry',
	jewelry_rings_left = 'jewelry',
	jewelry_bracelets = 'jewelry',
	aprons = 'aprons',
  pants = 'pants',
	skirts = 'skirts',
	belts = 'belts',
	belt_buckles = 'belt_buckles',
	gunbelts = 'gunbelts',
	holsters_left = 'holsters',
	boots = 'boots',
	boot_accessories = 'boot_accessories',
	spats = 'spats',
	chaps = 'chaps',
  badges = 'badges',
  gunbelt_accs = 'gunbelt_accs',
  hair_accessories = 'hair_accessories'
}

Config.Stores = {
	{ -- VALENTINE
		book = vector4(-326.17, 773.757, 117.5, -170.0), --location of the book
		fittingRoom = vector4(-329.31, 775.11, 120.63, 294.79), --location of the fitting room
		pedCoords = vector4(-325.67, 772.63, 116.44, 11.3), --location of the tailor ped
		pedModel = `S_M_M_Tailor_01`, --model of the tailor ped
		blip = true, --if the blip is displayed for this store
		distancePrompt = 2.0, --distance to display the prompt
		needInstance = true,
	},
}

Config.Wardrobes = {
	{
		location = vector3(1223.55, -1288.67, 76.9),
		blip = true,
		distancePrompt = 2.0,
		needInstance = false
	},
}

-- Price for each category
-- use -1 to turn off the category
Config.Prices = {
	coats_closed = 5,
	chaps = 4,
	spats = 5,
	ponchos = 4.25,
	holsters_left = 3.12,
	masks = 10,
	neckwear = 2.15,
	armor = 20,
	jewelry_rings_left = 1.25,
	jewelry_rings_right = 1.25,
	boot_accessories = 3.55,
	gloves = 4.25,
	badges = 2,
	gunbelts = 5,
	loadouts = 6.7,
	vests = 5,
	shirts_full = 5,
	pants = 5,
	suspenders = 1.5,
	gunbelt_accs = 1,
	hats = 3.5,
	cloaks = 5,
	coats = 5,
	belts = 2,
	gauntlets = 3,
	eyewear = 6,
	boots = 5,
	jewelry_bracelets = 2,
	satchels = 10,
	accessories = 2,
	neckties = 2,
	skirts = 5,
	belt_buckles = 1,
	dresses = 5
}

Config.modelPrices = {}
Config.modelPrices["male"] = {}
Config.modelPrices["female"] = {}
for category in pairs (Config.Prices) do
	Config.modelPrices["male"][category] = {}
	Config.modelPrices["female"][category] = {}
end
--Config.modelPrices[<sexe>][<category>][<number>] = <price>
Config.modelPrices["male"]["hats"][2] = Config.Prices.hats * 1.25
Config.modelPrices["male"]["hats"][3] = {money=2.75, gold = 2}
Config.modelPrices["male"]["hats"][4] = 5.5
Config.modelPrices["male"]["hats"][5] = 4.25
Config.modelPrices["male"]["hats"][6] = Config.Prices.hats * 2
Config.modelPrices["female"]["skirts"][6] = Config.Prices.hats * 2

--Function to buy item with gold for framework without native way to do it
Config.CanBuyWithGold = function (source,price)
	return false
end
```
:::

## 4. Custom Framework
⚠ Scripting skills are required to configure the script for custom framework ⚠

To use the script with a custom framework, you have to add some variables in the config file :
```lua
Config.Framework = "Custom" --Needed to unlock the custom framework feature

-------------------------
--- SERVER SIDE
-------------------------
--Function to get the identifier of player
--@param source is the serverID of the player
--@return array with identifier and charid key
Config.GetIdentifier = function(source)
    local player = {
        identifier = identifier, --the identifier of player
        charid = charid --the charid of player. If not needed just use ''
    }
    return player
end

--Function to check if the player has enough money to buy the cloth
--@param source is the serverID of the player
--@param price is the price of the cloth
--@param moneyType is the devise of the price : 0 for normal & 1 for gold
--@return true/false to accept/deny the purchase
Config.CanBuy = function(source,price, moneyType)
    return true
end

--Function to get the player's clothes
--@param source is the serverID of the player
--clothes is a table with clothing category in key and hash of cloth in value.
--clothes can be a json array
Config.GetClothes = function(source)
    local clothes = {}
    return clothes
end

--Function to get the player's skin
--@param source is the serverID of the player
--skin is a table with category in key and data in value.
Config.GetSkin = function(source)
    local skin = {}
    return skin
end

--Function fire to save the new cloth in the DB
--@param source is the serverID of the player
--@param dataPreview is a table with the new cloth data :
-- dataPreview.menu is the category of cloth
-- dataPreview.hash is the hash of cloth
Config.SaveNewCloth = function(source,dataPreview)
end

--Function fire when player select Outfit
--@param source is the serverID of the player
--@param clothes in the table with category in key and hash in value of the outfit
Config.ApplyNewOutfit = function(source,clothes)
end

--Function to send notification to player from serverside
--@param source is the serverID of the player
--@param text is the text to be sent to the player
Config.Notify = function(source, text)
end

--Function to send notification to player from serverside
--@param source is the serverID of the player
--@param amount is the amount of money to be sent to the player
Config.GiveMoney = function(source, amount)
end

--Function to give item from serverside
--@param source is the serverID of the player
--@param item is the item name
--@param quantity is the quantity of item
--@param meta is the meta of the item
Config.GiveItem= function(source,item,quantity,meta)
end

--Function to register a usable item from serverside
--@param item is the item name
--@param callback is the callback event with two arguments :
--callback(source,{hash = clothesHash})
Config.RegisterUseItem = function(item,callback)
end
```
## 5. For developers
You can open the wardrobe with this client event :
```lua
--@param needInstance = true/false : Define if the wardrobe need personnal instance
TriggerEvent('kd_clothingstore:openWardrobe', needInstance)
```
You can apply an outfit from his id to a player by trigger this server event (from client) :
```lua
TriggerServerEvent('kd_clothingstore:useOutfitId',id)
```
You can remove all clothes with this client event :
```lua
TriggerEvent('kd_clothingstore:removeAllClothes')
```
You can equip all clothes with this client event :
```lua
TriggerEvent('kd_clothingstore:resetClothes')
```
You can grab the closing of the menu after the ped creation with this client event :
```lua
kd_clothingstore:client:endCreation
```