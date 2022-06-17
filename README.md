# crazygame-plugin-construct2

Criei este plugin da engine construct 2 para poder usar a sdk de ad da plataforma crazy game, no site https://www.crazygames.com.

Ações no plugin:


- Init SDK (InitSDK): 

O que faz: Inicia a sdk da crazy games e precisa ser colocada numa ação a ser executada antes do anúncio, como por exemplo no start of layout.

Código na runtime:

 ```
	Acts.prototype.InitSDK = function ()
	{
	crazysdk.init() // initializing the SDK, call as early as possible

	};
 ```
