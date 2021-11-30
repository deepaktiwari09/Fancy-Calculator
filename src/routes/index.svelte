<script lang="ts">

    let list_of_n = [];
    let histry_list = [];
    let result = 0;
    let history_text = '';
    let is_full_history = false;
    function list_to_num(list){
        let resultt = ''
        for(let x=0; x<list.length; x++){
            resultt = resultt + list[x].toString();
        }
        return resultt
    }

    function list_toresult(list){
        let f_list = [];
        let s_list = [];
        let oprater = '';
        for(let x=0; x<list.length; x++){
            if (list[x] == "+"){
                oprater = "+";
                f_list = list.slice(0,x);
                s_list = list.slice(x,list.length);
            }
            if (list[x] == "-"){
                oprater = "-";
                f_list = list.slice(0,x);
                s_list = list.slice(x+1,list.length);
            }
            if (list[x] == "x"){
                oprater = "x";
                f_list = list.slice(0,x);
                s_list = list.slice(x+1,list.length);
            }
            if (list[x] == "/"){
                oprater = "/";
                f_list = list.slice(0,x);
                s_list = list.slice(x+1,list.length);
            }
            else{
                continue
            }
        
        }
        if(oprater == "+"){
            let f_n = list_to_num(f_list);
            let s_n = list_to_num(s_list);
            result =  parseInt(f_n) + parseInt(s_n);
            histry_list[histry_list.length] = list_to_num(list).toString() + "=" +result.toString();
            history_text = histry_list[histry_list.length-1]
        }
        if(oprater == "-"){
            let f_n = list_to_num(f_list);
            let s_n = list_to_num(s_list);
            result =  parseInt(f_n) - parseInt(s_n);
            histry_list[histry_list.length] = list_to_num(list).toString() + "=" +result.toString();
            history_text = histry_list[histry_list.length-1]
        }
        if(oprater == "x"){
            let f_n = list_to_num(f_list);
            let s_n = list_to_num(s_list);
            result =  parseInt(f_n) * parseInt(s_n);
            histry_list[histry_list.length] = list_to_num(list).toString() + "=" +result.toString();
            history_text = histry_list[histry_list.length-1]
        }
        if(oprater == "/"){
            
            let f_n = list_to_num(f_list);
            let s_n = list_to_num(s_list);
            result =  parseInt(f_n) / parseInt(s_n);
            histry_list[histry_list.length] = list_to_num(list).toString() + "=" +result.toString();
            history_text = histry_list[histry_list.length-1]
        }
        
        
    }

    

</script>
<main>
    <div class="m1">
        <h1>Calculator</h1>
    </div>
    {#if is_full_history == false}    
    <div class="m2">
        <div class="screen">
            
            {#each list_of_n as rl}
            <p>{rl}</p>
            {/each}
            <p>{history_text}</p>
            
        </div>
        <div class="board ">
            
                
                <button on:click="{()=>{list_of_n[list_of_n.length] = 1}}">1</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 2}}">2</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 3}}">3</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 4}}">4</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 5}}">5</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 6}}">6</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 7}}">7</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 8}}">8</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 9}}">9</button>
                <button on:click="{()=>{list_of_n[list_of_n.length] = 0}}">0</button>
                <button on:click="{()=>{list_of_n = []; history_text="",result=0;}}">Reset</button>
                <button class="for-b" on:click="{()=>{list_toresult(list_of_n);list_of_n = [];}}">=</button>
                <button class="for-b" on:click="{()=>{list_of_n[list_of_n.length] = "+"}}">+</button>
                <button class="for-b" on:click="{()=>{list_of_n[list_of_n.length] = "-"}}">-</button>
                
                
                <button class="for-b" on:click="{()=>{list_of_n[list_of_n.length] = "x"}}">x</button>
                <button class="for-b" on:click="{()=>{list_of_n[list_of_n.length] = "/"}}">/</button>
                
            
        </div>
        <div class="histry">
            <div>
                <p>Calculation History</p>
                <button on:click="{()=>{is_full_history = true;}}">Full History</button>
            </div>
            {#each histry_list.reverse().slice(0,7) as hl}
                <p>{hl}</p>
            {/each}
        </div>
    </div>
    {/if}
    {#if is_full_history == true}
        
    <div class="m3">
        <div class="m3_head">

            <button on:click="{()=>{is_full_history = false;}}">X</button>
        </div>
        <div class="m3_body">

            {#each histry_list.reverse().slice(0,45) as hl}
                <p>{hl}</p>
            {/each}
        </div>
    </div>
    {/if}

</main>
<style>
:root{
    --font-s1:36px;
    --font-s2:22px;
    --font-s3:18px;
    --font-s4:16px;
    --font-c:#291b03;
    --bg-c:#3b3103;
}
main{
    display: grid;
    place-content: center;
    
}
main>div{
    font-size: var(--font-s1);
    color: var(--font-c);
}
.m1{
    display:grid;
    place-content: center;
}
.m2{
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: .3fr 1fr;
    gap:1rem;

}
.m3{
    display:grid;
    grid-template-columns: 500px;
    grid-template-rows: 30px 1fr;
    /* width:100%; */
    height:100%;
    background-color: rgb(255, 255, 255);
    border-radius: 3rem;
    padding: 2rem;
    border:1px double black;
    animation-name: show;
    animation-duration:1000ms;
}
@keyframes show{
    0%{
        opacity:0%
    }
    100%{
        opacity:100%
    }
}

.screen{
    grid-column: 1/2;
    grid-row: 1/2;
    border-bottom: 1px dotted var(--bg-c);
    display:flex;
    justify-content: center;
}
.screen>p{
    animation-name: show;
    animation-duration:800ms;
}
.board{
    grid-column: 1/2;
    grid-row: 2/3;
    display: grid;
    place-content: center;
    grid-template-columns: repeat(4, 65px);
    grid-template-rows: repeat(6,50px);
    gap:1rem;
    
}
.board>button{
    /* margin-inline: 2rem; */
    display:flex;
    justify-content: center;
    align-items: center;
    border: 0px;
    font-size: var(--font-s2);
    color: var(--font-c);
    /* background-color: #fff0d7; */
}
.board>button:hover{
    
    background-color: var(--bg-c);
    color: white;
    animation-name: scale_it;
    animation-duration: 300ms;
    animation-fill-mode: forwards;
}
@keyframes scale_it{
    0%{
        transform:scale(100%);
        border-radius: 1rem;
    }
    100%{
        
        transform:scale(110%);
        border-radius: 2rem;
    }

}
.for-b{
    /* font-size: var(--font-s1); */
    font-weight: 600;
}
.histry{
    grid-column: 2/3;
    grid-row: 1/-1;
    /* background-color: yellowgreen; */
    display:flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    font-size: var(--font-s3);
    color:var(--font-c);
}
.histry>div{
    display:flex;
    justify-content: space-between;
    align-items: center;
}
.histry>div>button{
    cursor: pointer;
    margin-inline: 1rem;
    padding-inline:.5rem;
    padding-block:.3rem;
    border-radius: 1rem;
    border:1px solid black ;
    background-color: white;
}
.histry>div>button:hover{
    animation-name: scale_it;
    animation-duration: 300ms;
    animation-fill-mode: forwards;
}
.histry>p{
    animation-name: show;
    animation-duration:1000ms;
}
.m3_body{
    grid-column: 1/2;
    grid-row: 2/3;
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-template-rows: repeat(5,1fr);
    gap:1rem;
}
.m3_body>p{
    font-size: var(--font-s3);
    padding: 2px;
    border-radius: 1rem;
    background-color: var(--bg-c);
    color:white;
    font-weight: 600;
    display:grid;
    place-content:center;
}
.m3_head{
    grid-column: 1/2;
    grid-row: 1/2;
    display: flex;
    justify-content: end;
}
.m3_head>button{
    background-color: white;
    border: 0px;
    font-size: var(--font-s2);
    height: 100%;
    width:30px;
    padding: 2px;
    border-radius: 3rem;
    display:grid;
    place-content: center;
    cursor:pointer;
}

@media screen and (max-width:676px){
.m2{
    display: grid;
    grid-template-columns: 1fr ;
    grid-template-rows: .3fr 1fr 1fr;
    gap:1rem;
}
.histry{
    grid-column: 1/2;
    grid-row: 3/4;
    /* background-color: yellowgreen;
    display:flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    font-size: var(--font-s3);
    color:var(--font-c); */
}

}
</style>