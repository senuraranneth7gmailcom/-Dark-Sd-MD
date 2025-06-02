const { cmd } = require('../command')
const fs = require('fs');
const path = require('path');
const {readEnv} = require('../lib/githubdb')
const config = require('../config')

//auto_voice
cmd({
  on: "body"
},    
async (conn, mek, m, { from, body, isOwner }) => {
    const filePath = path.join(__dirname, '../data/autovoice.json');
    const data = JSON.parse(fs.readFileSync(filePath, 'utf8'));
    for (const text in data) {
        if (body.toLowerCase() === text.toLowerCase()) {
            const config = await readEnv();
            if (config.AUTO_VOICE === 'true') {
                if (isOwner) return;        
                await conn.sendPresenceUpdate('recording', from);
                await conn.sendMessage(from, { audio: { url: data[text] }, mimetype: 'audio/mpeg', ptt: true }, { quoted: mek });
            }
        }
    }                
});

//auto sticker 
cmd({
  on: "body"
},    
async (conn, mek, m, { from, body, isOwner }) => {
    const filePath = path.join(__dirname, '../data/autosticker.json');
    const data = JSON.parse(fs.readFileSync(filePath, 'utf8'));
    for (const text in data) {
        if (body.toLowerCase() === text.toLowerCase()) {
            const config = await readEnv();
            if (config.AUTO_STICKER === 'true') {
                if (isOwner) return;        
                await conn.sendMessage(from,{sticker: { url : data[text]},package: 'Queen-x'},{ quoted: mek })   
            
            }
        }
    }                
});

//auto reply 
cmd({
  on: "body"
},    
async (conn, mek, m, { from, body, isOwner }) => {
    const filePath = path.join(__dirname, '../data/autoreply.json');
    const data = JSON.parse(fs.readFileSync(filePath, 'utf8'));
    for (const text in data) {
        if (body.toLowerCase() === text.toLowerCase()) {
            const config = await readEnv();
            if (config.AUTO_REPLY === 'true') {
                if (isOwner) return;        
                await m.reply(data[text])
            
            }
        }
    }                
});                  

//auto recording
cmd({
  on: "body"
},    
async (conn, mek, m, { from, body, isOwner }) => {  
  const config = await readEnv();
     if (config.RECORDING === 'true') { 
        if (isOwner) return;
           await conn.sendPresenceUpdate('recording', from);
     }         
});

//auto react
cmd({
  on: "body"
},    
async (conn, mek, m, { from, body, isOwner }) => {  
  const config = await readEnv();
     if (config.AUTO_REACT === 'true') { 
        if (isOwner) return;
             await conn.sendMessage(from, { react: { text: '🌹', key: mek.key } });             
     }         
});
