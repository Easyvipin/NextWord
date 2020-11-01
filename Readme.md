### NextWord
This is a game app where you can play the game while chatting with your friends.

### Technologies
- [x] Socket.io

    Socket.io is library which wrap websocket protocol with extra features like sending packets with a meta data.
    
    Socket.io build full-duplex (bi-directional) connection between user and client and long polling connection when server rejects the websocket protocol upgrade.
    
    Bi-directional connectivity means the data can be send from server to client without making a request to the server and vice-versa.
    
    ###### installation
    server-side 
    
    `npm i socket.io`
    
    client-side 
    
    `npm i socket.io-client`
    
    ###### Working
   
     Socket.io work on two events `.emit( )`  and `.on( )`.
    
     .emit( ) triggers the events
     
     .on() listen to the events
     
     We can use both of these functions on client side as well as on server-side.
     
     See example here.
     
     client side (React)
     
     ```
     import React from "react";
     import io from "socket.io-client";
     const socket = io.connect("http://localhost:5000")
     class Arena extends React.Component {
      state = {
        connect : false,
        message : ""
   }
   onChange = (e) =>{
       this.setState({
           message:e.target.value
       })
   }
   onSubmit = (e) =>{
       e.preventDefault();
       socket.emit("chat message",this.state.message)
       this.setState({
           message:''
       })
       e.target.value = "";
   }
   
    render() { 
        return (
            <section className="msg-area">
            <div className="send-msg">
            <form onSubmit={this.onSubmit}>
            <input type="text" onChange={this.onChange}></input>
            <button type="submit">Send</button>
            </form>
            </div>
            <div className="see-message">
            {this.state.connect == true ? <p>Connected!!</p>:<p>Not Connected</p>}
            </div>
            </section>
        );
    }
    }
 
    export default Arena;
     ```
    Server-side (Express and node.js)
    
    ```
    const express = require('express');
    const app = express();
   const http = require("http");
   const server = http.createServer(app);
  const io =require("socket.io")(server);

   const PORT = process.env.PORT || 5000;

   io.on('connection',(socket)=>{
  const {id} = socket.client;
  console.log("socket connected");
  socket.on('chat message',(msg)=>{
  console.log(msg)
  console.log(`${id} : ` + msg);
  })
  })
  server.listen(PORT,()=>{
  console.log("connected.... :)")
  })
    ```
   Terminal output :
   
    ```
    socket connected
    hey all fine ?
   a0jCyM1gT4gWF-LOAAAA : hey all fine ?
    ```
