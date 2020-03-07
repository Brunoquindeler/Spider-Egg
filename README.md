# Spider-Egg
Script que transforma Spider Egg em Mobs no Open Tibia Server

Ao dar **USE** na **Spider Egg** ela é aberta e com chances de nascer algum tipo de Spider(spider, tarantula, poison spider, GS...) assim como acontece no global!

### TUTORIAL

- Crie um arquivo em actions /other com extensão .lua
- De o nome que desejar, no meu caso vou salvar como transformSpiderEgg.lua
- Copie e cole o código no arquivo criado

~~~lua
--[[Spider Egg
    --Classe:    Ferramentas (Objetos)
    --Atributos:    Sumona um monstro quando quebrado.
    --Adicionado:    Desconhecido.
    --Localização:    Cavernas de Spiders e Tarantula, encontradas em grande quantidade em Tiquanda.
    --Notas:    Spider Eggs são envolvidos por uma seda muito frágil e irão quebrar quando atacados. Muitas vezes, elas "libertam" uma Spider, uma Poison Spider, ou em casos raros uma Tarantula e em casos extremamente raros Giant Spiders.
    --Para quebrar o Spider Egg, simplesmente "use" o ovo.]]

--[[Spider Egg
    --Classification:    Natural Products
    --Attributes: Summon a monster when broken.
    --Add: Unknow
    --Location: Spider and Tarantula caves, such as those found in Tiquanda.
    --Notes: Spider Eggs are very fragile and will break when attacked. They will either release nothing, a Spider, a Poison Spider, a Tarantula at rare times and very rarely a Giant Spider. Spiders that come from those eggs will not puff like normal spiders do when taken away too far from their spawn point.
    --To break the Spider Egg, simply use the egg.]]

function onUse(player, item, fromPosition, target, toPosition, isHotkey)

math.randomseed(os.time())
n = math.random(0, 1000) -- Gera um número randomico de 0 a 1000 / Generates a random number from 0 to 1000


if n > 999 then
  Game.createMonster("Giant Spider", item:getPosition()) -- 1/1000 chance de nascer uma GS / chance to be born a GS
elseif n >= 985 then
  Game.createMonster("Tarantula", item:getPosition()) -- 15/1000 chance de nascer uma Tarantula / chance to be born a Tarantula
elseif n >= 900 then
  Game.createMonster("Poison Spider", item:getPosition()) -- 85/1000 chance de nascer uma PS / chance to be born a PS
elseif n >= 500 then
  Game.createMonster("Spider", item:getPosition()) --  400/1000 chance de nascer uma Spider / chance to be born a Spider
else
  fromPosition:sendMagicEffect(CONST_ME_POFF) -- 500/1000 chance dee falhar / chance of Fail
end

item:transform(7536) -- << ID DA remains of a spider egg | Transforma na remains of a spider egg / Transform on remains of a spider egg


function backInitialId() -- Função para voltar ao Id inicial / Function to return to the initial Id
item:transform(7537) -- << ID DA SPIDER EGG
end

addEvent(backInitialId, 30000) -- Volta a ser Spider Egg em 30 segundos / Back to Spider Egg in 30 seconds

end
~~~

#### Agora em actions, no actions.xml coloque a action com o ID da spider egg:
~~~xml
<action itemid="ID DA SPIDER EGG" script="other/transformsSpiderEgg.lua" />
~~~
