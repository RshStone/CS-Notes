`function showProductsAsideCategorys(cid){`
	`$("div.eachCategory[cid="+cid+"]").css("background-color","white");`
	`$("div.eachCategory[cid="+cid+"] a").css("color","#87CEFA");`
	`$("div.productsAsideCategorys[cid="+cid+"]").show();`
`}`

`function hideProductsAsideCategorys(cid){`
	`$("div.eachCategory[cid="+cid+"]").css("background-color","#e2e2e3");`
	`$("div.eachCategory[cid="+cid+"] a").css("color","#000");`
	`$("div.productsAsideCategorys[cid="+cid+"]").hide();`
`}`

`$(function(){`
    `$("div.eachCategory").mouseenter(function(){`
        `var cid = $(this).attr("cid");`
        `showProductsAsideCategorys(cid);`
    `});`
    `$("div.eachCategory").mouseleave(function(){`
        `var cid = $(this).attr("cid");`
        `hideProductsAsideCategorys(cid);`
    `});`
    `$("div.productsAsideCategorys").mouseenter(function(){`
    	`var cid = $(this).attr("cid");`
    	`showProductsAsideCategorys(cid);`
    `});`
    `$("div.productsAsideCategorys").mouseleave(function(){`
    	`var cid = $(this).attr("cid");`
    	`hideProductsAsideCategorys(cid);`
    `});`
`});`

