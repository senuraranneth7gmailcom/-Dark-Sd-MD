const { cmd, commands } = require('../command');
const config = require('../config');
const os = require('os');
const process = require('process');
const { exec } = require('child_process');
const { runtime } = require('../lib/functions');
const docxUrl = 'https://pomf2.lain.la/f/hxp64475.jpg';  // Make sure this URL is correct

//-----------------------------------------------ALive-----------------------------------------------

cmd({
    pattern: "alive",
    desc: "Check bot online or not.",
    category: "main",
    react: "👾",
    filename: __filename
},
async (conn, mek, m, { from, prefix, pushname, reply }) => {
    try {
        // Fetch the configuration/environment settings
        const config = await readEnv();  // Ensure readEnv returns a promise if needed

        // Determine the host platform
        let hostname = os.hostname();
        if (hostname.length == 12) hostname = 'replit';
        else if (hostname.length == 36) hostname = 'heroku';
        else if (hostname.length == 8) hostname = 'koyeb';

        const snm = [2025];
        const qMessage = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
                orderMessage: {
                    itemCount: snm[Math.floor(Math.random() * snm.length)],
                    status: 1,
                    surface: 1,
                    message: `✨ 𝐐𝐮𝐞𝐞𝐧 𝐗 𝐌𝐃 𝐖𝐡𝐚𝐭𝐬𝐚𝐩𝐩 𝐁𝐨𝐭 𝐁𝐲 -:\n𝐍𝐞𝐭𝐡𝐮 𝐌𝐚𝐱 𝐘𝐭...💗`,
                    orderTitle: "",
                    sellerJid: '94704227534@s.whatsapp.net'
                }
            }
        };


        // Create the text response with system details
        const monspace = '```';
        const sssf = `${monspace}👋 Hello ${pushname}, I'm alive now${monspace}

> *Version:* ${require("../../package.json").version}
> *Memory:* ${(process.memoryUsage().heapUsed / 1024 / 1024).toFixed(2)}MB / ${(os.totalmem() / 1024 / 1024).toFixed(2)}MB
> *Runtime:* ${runtime(process.uptime())}
> *Platform:* ${hostname}

*🔢 Reply Below Number:*

1 || View Bot Speed
2 || Contact Bot Owner

*👨‍💻 Qᴜᴇᴇɴ x ᴍᴅ ʙʏ ɴᴇᴛʜᴜ ᴍᴀx ʏᴛ 👨‍💻*
`;

        // Send the audio message
        await conn.sendMessage(from, {
            audio: { url: 'https://github.com/NETHU-MAX/QUEEN-X-DATABASE/raw/refs/heads/main/media/alive%20.mp3' },
            mimetype: 'audio/mp4',
            ptt: true
        }, {quoted:qMessage});
        
        // Send the document (PDF) message with the caption
        const sentMsg = await conn.sendMessage(from, {
            document: { url: docxUrl },  // Ensure this URL is correct and accessible
            fileName: '𝚀𝚄𝙴𝙴𝙽 𝚇 𝙼𝙳',  // Filename for the document
            mimetype: "application/docx",
            fileLength: 99999999999999,  // Replace with the actual size if possible
            caption: sssf,  // Add a caption to the message
            contextInfo: {
                forwardingScore: 999,
                isForwarded: true,
                forwardedNewsletterMessageInfo: {
                    newsletterName: 'ɴᴇᴛʜᴜ ᴍᴀx ʏᴛ',
                    newsletterJid: "120363322195409882@newsletter",
                },
                externalAdReply: {
                    thumbnailUrl: 'https://pomf2.lain.la/f/hxp64475.jpg',  // Ensure this image is accessible
                    sourceUrl: 'https://www.youtube.com/@SlNethuMax',
                    title: '𝚀𝚄𝙴𝙴𝙽 𝚇 𝙼𝙳',
                    body: 'ᴅᴇᴠᴇʟᴏᴘᴇʀ ʙʏ ɴᴇᴛʜᴍɪᴋᴀ ᴋᴀᴜꜱʜᴀʟʏᴀ',
                    mediaType: 1,
                    renderLargerThumbnail: true
                }
            }
        }, {quoted:qMessage});

        // Listen for User Response
        conn.ev.on('messages.upsert', async (msgUpdate) => {
            const userMsg = msgUpdate.messages[0];
            if (!userMsg.message || !userMsg.message.extendedTextMessage) return;

            const selectedOption = userMsg.message.extendedTextMessage.text.trim();

            // Validate if the response matches the `.alive` message
            if (
                userMsg.message.extendedTextMessage.contextInfo &&
                userMsg.message.extendedTextMessage.contextInfo.stanzaId === sentMsg.key.id
            ) {
                try {
                    switch (selectedOption) {
                        case '1': {
                            const startTime = Date.now();
                            const message = await conn.sendMessage(from, { text: '```Pinging To index.js!!!```' });
                            const endTime = Date.now();
                            const ping = endTime - startTime;

                            // Send the ping response without buttons
                            await conn.sendMessage(from, { text: `*Pong*\n*${ping}ms*` }, { quoted: qMessage });
                            break;
                        }
                        case '2': {
                            try {
                                const vcard = 'BEGIN:VCARD\n' 
                                    + 'VERSION:3.0\n' // Changed to 3.0 for more modern support
                                    + 'FN:Mr. Nethmika\n'
                                    + 'ORG:Mr. Nethmika\n'
                                    + 'TEL;type=CELL;type=VOICE;waid=94704227534:+94 70 422 7534\n'
                                    + 'EMAIL:nethmika90@gmail.com\n'
                                    + 'END:VCARD';

                                await conn.sendMessage(from, { 
                                    contacts: { 
                                        displayName: 'Mr. Nethmika', 
                                        contacts: [{ vcard }] 
                                    }
                                }, { quoted: qMessage });

                                break;

                            } catch (e) {
                                console.error(e);
                                await conn.sendMessage(from, { text: "*❌ Error processing your request.*" }, { quoted: userMsg });
                            }
                            break;
                        }
                    }
                } catch (e) {
                    console.error(e);
                }
            }
        });
    } catch (err) {
        console.error(err);
        await reply('An error occurred.');
    }
});

//-----------------------------------------------Owner-----------------------------------------------

cmd({
    pattern: "owner",
    react: "👑", // Reaction emoji when the command is triggered
    desc: "Get owner number",
    category: "main",
    filename: __filename
}, 
async (conn, mek, m, { from }) => {
    try {
        // Array of item counts to randomly select from
        const snm = [2025];
        
        // The quoted message template
        const qMessage = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
                orderMessage: {
                    itemCount: snm[Math.floor(Math.random() * snm.length)], // Random selection
                    status: 1,
                    surface: 1,
                    message: `✨ 𝐐𝐮𝐞𝐞𝐧 𝐗 𝐌𝐃 𝐖𝐡𝐚𝐭𝐬𝐚𝐩𝐩 𝐁𝐨𝐭 𝐁𝐲 -:\n𝐍𝐞𝐭𝐡𝐮 𝐌𝐚𝐱 𝐘𝐭...💗`,
                    orderTitle: "",
                    sellerJid: '94704227534@s.whatsapp.net'
                }
            }
        };

        // Owner's contact info in vCard format
        const vcard = 'BEGIN:VCARD\n' 
            + 'VERSION:3.0\n' // Use version 3.0 for better compatibility
            + 'FN:Mr. Nethmika\n'
            + 'ORG:Mr. Nethmika\n'
            + 'TEL;type=CELL;type=VOICE;waid=94704227534:+94 70 422 7534\n'
            + 'EMAIL:nethmika90@gmail.com\n'
            + 'END:VCARD';

        // Sending the contact info as a WhatsApp message
        await conn.sendMessage(from, { 
            contacts: { 
                displayName: 'Mr. Nethmika', 
                contacts: [{ vcard }] 
            }
        }, { quoted: qMessage });

    } catch (error) {
        console.error('Error occurred while fetching the owner contact:', error);
        
        // If there's an error, send a user-friendly error message
        await conn.sendMessage(from, { text: 'Sorry, there was an error fetching the owner contact.' }, { quoted: mek });
    }
});


//-----------------------------------------------Pong-----------------------------------------------

cmd({
    pattern: "ping",
    desc: "Check bot's response time.",
    category: "main",
    react: "🪄",
    filename: __filename
}, async (conn, mek, m, { from, quoted, reply }) => {
    try {
        const snm = [2025]; // Random number array, only one item here
        const qMessage = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
                orderMessage: {
                    itemCount: snm[Math.floor(Math.random() * snm.length)],
                    status: 1,
                    surface: 1,
                    message: `✨ 𝐐𝐮𝐞𝐞𝐧 𝐗 𝐌𝐃 𝐖𝐡𝐚𝐭𝐬𝐚𝐩𝐩 𝐁𝐨𝐭 𝐁𝐲 -:\n𝐍𝐞𝐭𝐡𝐮 𝐌𝐚𝐱 𝐘𝐭...💗`,
                    orderTitle: "",
                    sellerJid: '94704227534@s.whatsapp.net'
                }
            }
        };

        const startTime = Date.now();
        const message = await conn.sendMessage(from, { text: '```Pinging To index.js!!!```' });
        const endTime = Date.now();
        const ping = endTime - startTime;

        // Send the ping response without buttons
        await conn.sendMessage(from, { text: `*Pong*\n*${ping}ms*` }, { quoted: qMessage });
    } catch (e) {
        console.error(e);
        reply(`Error: ${e.message}`);
    }
});


//-----------------------------------------------System-----------------------------------------------

cmd({
    pattern: "system",
    alias: ["os"],
    desc: "check up time",
    category: "main",
    react: "👀",
    filename: __filename
},
async (conn, mek, m, { from, quoted, body, isCmd, command, args, q, isGroup, sender, senderNumber, botNumber2, botNumber, pushname, isMe, isOwner, groupMetadata, groupName, participants, groupAdmins, isBotAdmins, isAdmins, reply }) => {
    try {
        const snm = [2025]; // Random number array, only one item here

        // Make sure qMessage has a valid structure
        const qMessage = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
                orderMessage: {
                    itemCount: snm[Math.floor(Math.random() * snm.length)],
                    status: 1,
                    surface: 1,
                    message: `✨ 𝐐𝐮𝐞𝐞𝐧 𝐗 𝐌𝐃 𝐖𝐡𝐚𝐭𝐬𝐚𝐩𝐩 𝐁𝐨𝐭 𝐁𝐲 -:\n𝐍𝐞𝐭𝐡𝐮 𝐌𝐚𝐱 𝐘𝐭...💗`,
                    orderTitle: "",
                    sellerJid: '94704227534@s.whatsapp.net'
                }
            }
        };

        let hostname = os.hostname();
        if (hostname.length === 12) hostname = 'replit';
        else if (hostname.length === 36) hostname = 'heroku';
        else if (hostname.length === 8) hostname = 'koyeb';

        // Function to convert seconds to human-readable format
        const runtime = (seconds) => {
            const pad = (s) => s < 10 ? `0${s}` : s;
            const hours = Math.floor(seconds / (60 * 60));
            const minutes = Math.floor((seconds % (60 * 60)) / 60);
            const sec = Math.floor(seconds % 60);
            return `${pad(hours)}:${pad(minutes)}:${pad(sec)}`;
        };

        let status = `
*╭────────────────────*
*│🚀Version :* ${require("../package.json").version}  
*│⌛Ram usage :* ${(process.memoryUsage().heapUsed / 1024 / 1024).toFixed(2)}MB / ${Math.round(os.totalmem() / 1024 / 1024)}MB
*│🕒Runtime :*  ${runtime(process.uptime())}
*│📍Platform :* ${hostname}
*│👨‍💻Owner :* ɴᴇᴛʜᴜ ᴍᴀx ʏᴛ  
*╰────────────────────*`;

        // Ensure proper `sendMessage` with quoted message, fallback to qMessage if none
        const messageToSend = { text: `${status}` };
        const options = quoted ? { quoted: quoted } : { quoted: qMessage };

        await conn.sendMessage(from, messageToSend, options);
    } catch (e) {
        console.log(e);
        reply(`${e.message || e}`);
    }
});


//-----------------------------------------------Repo-----------------------------------------------

cmd({
    pattern: "repo",
    alias: ["sc","script"],
    desc: "Check Bot Sc",
    category: "main",
    react: "🌟",
    filename: __filename
}, async (conn, mek, m, { from, quoted, body, isCmd, command, args, q, isGroup, sender, senderNumber, botNumber2, botNumber, pushname, isMe, isOwner, groupMetadata, groupName, participants, groupAdmins, isBotAdmins, isAdmins, reply }) => {
    try {
        // Create a status message to be sent
        const desc = `*🧚‍♂️ 𝘘𝘜𝘌𝘌𝘕 𝘟 𝘔𝘋 𝘖𝘍𝘍𝘐𝘊𝘐𝘈𝘓 🧚‍♂️*

🔮 The main hope of creating this bot is to take full advantage of the WhatsApp app and make its work easier


💡 Various things can be downloaded from this bot.  Also, managing groups, making logos & edit-images in different ways, searching for different things and getting information and more futures included.


⚠️ Also, if your Whatsapp account gets damaged or banned by using this, we are not responsible and you should take responsibility for it.


🪀 You can create the bot and see the deploy methods from the website below.👇


💃 *Owner :* Nethmika Kaushalya

🎡 *Github :* https://github.com/

🧿 *Yt channel :* https://www.youtube.com/@SlNethuMax

🪄 *Our channel :* https://whatsapp.com/channel/0029VagCogPGufJ3kZWjsW3A

*👨‍💻 Qᴜᴇᴇɴ x ᴍᴅ ʙʏ ɴᴇᴛʜᴜ ᴍᴀx ʏᴛ 👨‍💻*`;

        // Sending the message with an image (thumbnail)
        const sentMsg = await conn.sendMessage(from, {
            image: { url: 'https://pomf2.lain.la/f/hxp64475.jpg' },  // Sending an image (URL)
            caption: desc,  // Send the description as the caption
            contextInfo: {
                forwardingScore: 999,
                isForwarded: true,
                forwardedNewsletterMessageInfo: {
                    newsletterName: 'ɴᴇᴛʜᴜ ᴍᴀx ʏᴛ',
                    newsletterJid: "120363322195409882@newsletter",
                },
                externalAdReply: {
                    title: '',
                    body: '',
                    mediaType: 1,
                    sourceUrl: "https://www.youtube.com/@SlNethuMax",
                    thumbnailUrl: 'https://pomf2.lain.la/f/hxp64475.jpg', // Corrected thumbnail URL
                    renderLargerThumbnail: false,
                    showAdAttribution: true
                }
            }
        }, { quoted: mek });
    } catch (e) {
        console.error(e);
        reply(`*Error:* ${e.message}`);
    }
});

//---------------------------------Restart-----------------------------------

cmd({
    pattern: "restart",
    react: "♻",
    desc: "restart the bot",
    category: "owner",
    filename: __filename
},
async (conn, mek, m, { from, quoted, body, isCmd, command, args, q, isGroup, sender, senderNumber, botNumber2, botNumber, pushname, isMe, isOwner, groupMetadata, groupName, participants, groupAdmins, isBotAdmins, isAdmins, reply }) => {
    try {
        // Ensure that only the owner can use this command
        if (!isOwner) return reply("This command is restricted to the bot owner.");

        // Create a custom message that will be used for the quoted message
        const snm = [2025];
        const qMessage = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
                orderMessage: {
                    itemCount: snm[Math.floor(Math.random() * snm.length)],
                    status: 1,
                    surface: 1,
                    message: `✨ 𝐐𝐮𝐞𝐞𝐧 𝐗 𝐌𝐃 𝐖𝐡𝐚𝐭𝐬𝐚𝐩𝐩 𝐁𝐨𝐭 𝐁𝐲 -:\n𝐍𝐞𝐭𝐡𝐮 𝐌𝐚𝐱 𝐘𝐭...💗`,
                    orderTitle: "",
                    sellerJid: '94704227534@s.whatsapp.net'
                }
            }
        };

        // Define a sleep function using promises
        const sleep = (ms) => new Promise(resolve => setTimeout(resolve, ms));

        // Send the restarting message
        await conn.sendMessage(from, { text: `*Restarting...*` }, { quoted: qMessage });

        // Sleep for 1500ms (1.5 seconds) before restarting the bot
        await sleep(1500);

        // Execute the restart command
        const { exec } = require("child_process");
        exec("pm2 restart all", (error, stdout, stderr) => {
            if (error) {
                console.error(`exec error: ${error}`);
                reply(`Error restarting the bot: ${stderr}`);
                return;
            }
            console.log(`stdout: ${stdout}`);
            console.log(`stderr: ${stderr}`);
        });
        
    } catch (e) {
        console.log(e);
        reply(`${e}`);
    }
});

//-----------------------------------
