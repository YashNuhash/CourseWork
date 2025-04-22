# YouTube Script: XOR - Real-time Code Collaboration Made Easy

## Intro (1 minute)
"Hey everyone! What's up? Today I'm wanna to show you something what we've been working on - that XOR, a real-time code collaboration tool. You know those moments when you're trying to debug with your teammate and sharing code is a mess? Yeah, So we created XOR. Let me show you how it works!

## Landing Page (1-2 minutes)
[Show landing page with animations]
Ok let's go to this domain , it's on the description , "Check this out - this is a Pretty cool home page, then click start collaborating button

## Getting Started (1-2 minutes)
"Alright, let's jump in! All you need to do is:
- Click this 'Start Collaborating' button
- Type in your name
- Boom! You get a room ID

Super simple, no signup needed. Share this room ID with your friend and you're ready to code together!

## Live Demo (2-3 minutes)
[Open two browser windows side by side]
"Now here's where it gets interesting. I'm gonna open another tab to show you how this works in real-time. 

Let's write some code... [Start typing in one window]
Look at that - instant sync! Whatever I type here shows up immediately in the other window. No lag, no delays.

And check out these language options:
- JavaScript/TypeScript
- Python
- Java
- HTML/CSS
And more... all with proper syntax highlighting!

## Cool Features (2 minutes)
"But wait, there's more! Let me show you some features I'm really proud of:

1. Look at these profile avatars - you can see who's in the room
2. Copy room ID with one click
4. And my favorite - real-time code sync with zero delay

## Technical Bits (1 minute)
"For the nerds out there wondering how this works:
- Frontend: Next.js and TypeScript
- Backend: Node.js with Socket.IO for that sweet real-time action
- UI: Tailwind CSS because, come on, it's awesome
- All hosted on Vercel and Render


Don't forget to check out the repo on GitHub, and let me know what features you'd like to see next!

## Call to Action
"If you found this helpful, smash that like button and subscribe for more cool projects like this. Drop a comment if you want me to explain any part in detail.

Peace out! ✌️"

## B-Roll Suggestions:
1. Smooth transitions showing:
   - Landing page animations
   - Code syncing in action
   - Multiple users coding together
   - Language switching
   - Mobile responsiveness

2. Close-up shots of:
   - Syntax highlighting
   - Real-time updates
   - UI animations
   - Profile system

3. Split-screen demonstrations showing:
   - Real-time collaboration
   - Different devices/screen sizes
   - Multiple users in the same room


## Technical Deepdive : 

I'll explain the "Last Write Wins" conflict resolution strategy used in XOR with a practical example.

Let's create a scenario with two users in the same room:

Scenario:

Example Timeline
`Room ID: abc-123
Users: Alice and Bob
Initial Code: empty
`
Initial State (Empty editor):
Alice Types (t = 1s):
`function hello()`
Bob Types (t = 1.2s):
`function greet()`
Alice Continues (t = 1.5s):
`function hello() {
    console.log("Hello");
}
`
Bob Continues (t = 1.7s):
`
function greet() {
    console.log("Hi");
}
`
How Last Write Wins Works in XOR:
In the code, this is handled by Socket.IO events:
`
// In server.cjs
socket.on("codeChange", ({ roomId, code }) => {
    if (roomCode[roomId] !== undefined) {
        // Last write wins: Simply overwrite the previous code
        roomCode[roomId] = code;
        // Broadcast to other users
        socket.to(roomId).emit("codeUpdate", code);
    }
});
`
What Happens:
When Alice types, it sends a codeChange event
When Bob types, it also sends a codeChange event
The server processes these events in order of arrival
Each new code update completely replaces the previous state
All users in the room receive the latest state
So in our example:

If Bob's last change (t = 1.7s) arrives last, everyone will see:
`
function greet() {
    console.log("Hi");
}
`

If Alice's last change (t = 1.5s) arrives last, everyone will see:
`
function hello() {
    console.log("Hello");
}
`
Benefits of Last Write Wins:
   - Simple to implement
   - No complex merge logic
   - Predictable behavior
   - Low latency
Limitations:
- Can lose changes if users edit the same section
- Not suitable for long-form collaborative editing
- Best for short-term collaborations or demonstrations

This simple approach works well for XOR because:

Coding sessions are typically short
- Users usually coordinate verbally/chat
- Real-time feedback shows others' changes immediately
- Users can see who else is in the room
- Perfect for pair programming scenarios 


So thanks for watching; The repository link in the description ; 
