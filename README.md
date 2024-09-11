my first plugin 
<?php

use pocketmine\plugin\PluginBase;
use pocketmine\event\Listener;
use pocketmine\event\player\PlayerInteractEvent;
use pocketmine\inventory\ChestInventory;
use pocketmine\item\ItemStack;
use pocketmine\item\Item;
use pocketmine\utils\TextFormat;

class GUIButtonPlugin extends PluginBase implements Listener {

    public function onEnable() {
        $this->getServer()->getPluginManager()->registerEvents($this, $this);
    }

    public function onInteract(PlayerInteractEvent $event) {
        $player = $event->getPlayer();
        $block = $event->getBlock();

        if ($block->getId() === Item::CHEST) {
            $inventory = new ChestInventory(45, TextFormat::BOLD . "GUI Buttons");
            $inventory->setItem(0, ItemStack::of(Item::DIAMOND_SWORD, 1, 0, ["lore" => ["Button 1"]]));
            $inventory->setItem(1, ItemStack::of(Item::GOLDEN_APPLE, 1, 0, ["lore" => ["Button 2"]]));
            $inventory->setItem(2, ItemStack::of(Item::EMERALD, 1, 0, ["lore" => ["Button 3"]]));
            $inventory->setItem(3, ItemStack::of(Item::ENDER_PEARL, 1, 0, ["lore" => ["Button 4"]]));
            $player->openInventory($inventory);
        }
    }
}
