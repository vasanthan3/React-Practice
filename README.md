
import {useState,useRef,useEffect} from "react";
export default function App() { 
    const[val,setVal]=useState({
        name:"",
        mobile:"",
        password:""
    });
    const[sub,setSub]=useState([]);
    const[alert,setAlert]=useState("");
    const inputRef = useRef(null); 
      const [isChecked, setIsChecked] = useState(false);
    const[isClick,setIsClick]=useState(false);

  const checkHandler = () => {
    setIsChecked(!isChecked);
  }

    
    function handle(e){
                console.log(e.target.value);
              setVal(prev=> ({ ...prev, [e.target.name]: e.target.value }));  
    
    }

  const handleClick = () => {
    // Select all the text in the input field when the button is clicked
    inputRef.current.focus();
  };

    const pop=()=>{
        setIsClick(false);
    }
    

    function subm(e){
        e.preventDefault();
            if(val.mobile.length==10){
                       setSub(prev=>([...prev,val]));
                    setVal({
                                name:"",
                                mobile:"",
                                password:""
                        
                    });  
                setAlert("");
                setIsClick(true);

                setTimeout(()=>{
                     setIsClick(false);
                },10000);
            }
            else{
             setAlert("*Mobile no Should be in 10 Digit*");
            }

    }

  return (
      <>
      <form onSubmit={subm}>
                   <label sty>Name:  </label>
                    <input type="text" ref={inputRef} onChange={handle} value={val.name} name="name" required/> <br></br> 
                       <br></br>
          <label>Mobile:</label>
                    <input type="text" onChange={handle} value={val.mobile} name="mobile" required/> <br></br>
                    <span style={{color:"red"}}>{alert}</span>    <br></br>
            <label>Password:</label>
          <input type={isChecked?"text" : "password"} name="password" onChange={handle} value={val.password}/> 
          <input type="checkbox" onChange={checkHandler} checked={isChecked} /> <br></br>
          <button onClick={handleClick}>Submit</button>
         
      </form>
         <br></br>
          <br></br>
      {
              sub.length>0 &&
              <table  border="2px" style={{borderCollapse:"collapse"}} cellpadding="3px">
                  <thead>
                      <th>Name</th>
                      <th>Mobile</th>
                      <th>Password</th>
                  </thead>
                <tbody>
                    {
                        sub.map((data,index)=>(
                            <tr key={index}>
                                <td>{data.name}</td>
                                <td>{data.mobile}</td>
                                <td>{data.password}</td>
                            </tr>
                        ))
                    }
                </tbody>
              </table>
    }
        

          {
          <div class="base" style={{opacity:isClick?1:0}}>
              Succesfully Register
              <div class="sub" onClick={pop}>
                  <div class="child"></div>
                  <div class="child low"></div>
              </div>
              <div class={isClick?"progress":" "}  ></div>
          </div>
      }
    </>
      
  )
}
------------------------------------------------------------------------------------
body {
  font-family: sans-serif;
  -webkit-font-smoothing: auto;
  -moz-font-smoothing: auto;
  -moz-osx-font-smoothing: grayscale;
  font-smoothing: auto;
  text-rendering: optimizeLegibility;
  font-smooth: always;
  -webkit-tap-highlight-color: transparent;
  -webkit-touch-callout: none;
}

h1 {
  font-size: 1.5rem;
}

form{
    display:inline-block;
    background-color:#102770;
    padding:20px;
    border-radius:9px;
}

label{
    color:white;
}

.base{
    background-color:green;
    display:inline-block;
    color:white;
    padding:20px 40px;
    font-weight:500;
    font-family:arial;
    font-size:20px;
    position:relative;
    top:40px;
}

.sub{
    width:20px;
    height:30px;
    position:absolute;
    top:-30px;
    right:-9px;
    cursor:pointer;
}

.child{
    background-color:black;
    width:4px;
    height:25px;
    transform:rotate(36deg);
}

.low{
    transform:rotate(-36deg);
    position:absolute;
    bottom:5px;
}

.progress {
  width: 100%;
  height: 4px;
  background-color: red;
  position: absolute;
  bottom: 0;
  left: 0;
  animation: example 10s linear forwards; 
}

@keyframes example {
  from {
    width: 100%;
  }
  to {
    width: 0%;
  };

input[type="checkbox"]{
    margin-top:10;
}


---------------------------------------------------------------------------------------
