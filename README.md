


var time = 80;      //rapidité du random
var initTime = 1000;//temps a l'init
var over = true;  //valeur true le hover fonctionne 


var originalString =[]; //tableau pour stocker les valeurs des diff chaine de caracteres
	spin=false;			



var init = function(element){
	
	$(element).data('original',$(element).html()); 
	
	
}

var run = function(element){
	var that = element; // pareil que this
	spin = setInterval(function(){
		nword(that);
	}, time); // var qui va changer les lettre, 1 lettre tt les 20 ms	
	$(element).data('spin',spin); 
}


var blend = function(element){
	
	var strLength = $(element).html().length;
	var rdm = "0123456789abcdefghijklmnopqrstuvwxyz#+=$*£%§";
	var rdmstring ='';
	
	for(i=0 ; i< strLength; i++){
		if($(element).html()[i] != ' '){
			var num = Math.floor(Math.random() * rdm.length);
			rdmstring += rdm.substring(num, num+1);
		}
		else{
			rdmstring +=' ';
		}
		
	}
	return rdmstring;
	
}

var nword = function(element){
	
	var stupidString = blend(element);
	
	$(element).html(stupidString);
	
}

var reset = function(element){
	
	clearInterval($(element).data('spin')); 
	$(element).html($(element).data('original'));
}


$(document).ready(function(){
	if(over == true){
		$('.titre').hover(//fonctionne qd on passe sur le titre
	
		function(){
			
			init(this);
			run(this);
			
		},
		
		function(){
			
			reset(this);
			
		}
	);
	}
	
	$('.titre').each(function(){
		init(this);
		run(this);
		
		var self = this;
		window.setTimeout(function(){
			reset(self);
		},initTime)
		
		
		
		
	});	
	
});
