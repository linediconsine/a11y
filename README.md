# a11y
Accessibily code snippets

## Web accessibility snippets of code

### Keyboard focus - Work in Progress

~~~javascript
/* 
	v0.1 alpha - Thsi is a work in progress
	
	Allow keyboard focus using anchor element :
		<a href="#targetid">move keyboard focus to element</a>
	
	- no jQuery required
	- use tabindex 
	 
 */
const elementList = document.querySelectorAll("a[href^='#']");
elementList.forEach(function(_anchor) {
    const _anchor_href = _anchor.getAttribute("href").slice(1);


    _anchor.addEventListener("click", function(me){

            let _target_elem = null;

            if(_anchor_href == "skipToMainContent"){
              _target_elem = document.querySelector("h1");

            }
            if(_target_elem === null){
               _target_elem = document.getElementById(_anchor_href);
            }

            //console.log("_target_elem " +  _target_elem)

            if(_target_elem.hasAttribute("tabindex")){

                const temp_tabindex_original = _target_elem.getAttribute("tabindex");
                _target_elem.removeAttribute("tabindex");

                _target_elem.setAttribute("tabindex", "0");
                _target_elem.focus();

                setTimeout(function(){
                    window.location.hash = "";
                    _target_elem.setAttribute("tabindex", temp_tabindex_original);
                }, 500);

            }else{
                //console.log("tabindex");
                _target_elem.setAttribute("tabindex", "0");
                _target_elem.focus();

                //setTimeout(function(){
                    //window.location.hash = "";
                    //_target_elem.removeAttribute("tabindex");
                //}, 500);

                }
    });
});
~~~
