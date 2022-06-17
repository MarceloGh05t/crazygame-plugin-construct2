# crazygame-plugin-construct2

Criei este plugin da engine construct 2, que permite usar a sdk de ad da plataforma crazy game, no site https://www.crazygames.com.

Ações no plugin:


- Init SDK (InitSDK): 

O que faz: Inicia a sdk da crazy games e precisa ser colocada numa ação a ser executada antes do anúncio, como por exemplo no start of layout.

Código na runtime:

 ```
//também tem o código da sdk deles, como é extensão não coloquei aqui, mas pode ser acessada no link: https://sdk.crazygames.com/crazygames-sdk-v1.js baseado na doc do link: https://docs.crazygames.com/sdk/html5/
 const crazysdk = window.CrazyGames.CrazySDK .getInstance(); // getting the SDK
 
	Acts.prototype.InitSDK = function ()
	{
	crazysdk.init() // initializing the SDK, call as early as possible

	};
 ```
 
- Request Ads (ShowAds):

O que faz: Depois que a sdk for incializada vai requesitar um anúncio e exebir em seguida, depois cria gatilhos para quando a requisiçao do anúncio e quando ele for exibidos para poder serem usados nas comparações. No modo preview do construct2 vai mostrar uma imagem no lugar do anúncio, mas na QATool da game crazy dá pra testar em tempo real, usando iframe e o link do localhost, que o construct gera no preview.

Código na runtime:

 ```
 function adFinished (){
    crazysdk.adRequested = false;
	crazysdk.adStarted = false // add este para comparar tnato pelo requisicao da ad ou quando o anuncio realmente começa
  };  
  
function adStarted () {
    crazysdk.adStarted = true; // antes eles faziam o som parar neste momento so add a condicao verdadeira para poder colocar na condicao quando a ad aparecer, ja q tem um lag de quando é solicitada
  };
  
 	Acts.prototype.ShowAds = function ()
	{
	crazysdk.adRequested = true;
	crazysdk.requestAd("midgame");
	crazysdk.addEventListener("adFinished", adFinished) // vai add o evento "adFinished" e quando foi acionado chama a funcao adFinished
	crazysdk.addEventListener("adStarted", adStarted) // vai add o evento "adStarted" e quando foi acionado chama a funcao adStart
	}
 ```
 
 Condições no plugin:
 
- Ad Requested (adRequested):

O que faz: verifica se foi requisitada uma propaganda (ad) para poder ser criada ação de mutar o som da app ou jogo e parar o tempo. Porém como pode exister um tempo de resposta para o anúncio aparecer.

Código na runtime:
 
 ```
 Cnds.prototype.adRequested = function ()
	{
	if(crazysdk.adRequested){
		  
		return true
	}	
	};
 ```

- Ad Started (adStarted):

O que faz: checa se a propaganda (ad) começou, ela pode ser usada do lugar da condição ad Requested, pois só é acionada com o surgimento da propaganda.

Código na runtime:

 ```
 Cnds.prototype.adStarted = function ()
	{
	if(crazysdk.adStarted){
			
		return true
	}
	};

 ```
 
- Ad Finished (adFinished):

O que faz: checa se a propaganda terminou para poder criar ações para o volume do app ou jogo voltar e voltar o tempo para a escala normal.

Código na runtime:

 ```
 Cnds.prototype.adFinished = function ()
	{
	if(crazysdk.adRequested === false){
		
		return true
	}	
	};
 ```
