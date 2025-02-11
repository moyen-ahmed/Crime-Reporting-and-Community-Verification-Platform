# CRIME REPORTING AND COMMUNITY VERIFICATION PLATFORM 
**NSU Tech Fest 2025 HACKATHON** - organized by Programming Hero **|** 12 February 2025 **|** North South University


> WEB APPLICATION that allows users to 
> - REPORT CRIMES in their area
> - ATTACH EVIDENCE (images/videos)
> - ENABLE THE COMMUNITY to verify the authenticity of the reports through upvotes, downvotes, and comments with mandatory proof attachments
> - The platform will also include AI-GENERATED DESCRIPTIONS for uploaded images, user authentication, and 
> - A ROBUST SYSTEM for filtering, sorting, searching crime reports

## Team - TECHNERANTS 
- Ishtiak Ahmed Moyen <sub> `moyen-ahmed`
- S. M. Karimul Hassan <sub> `depressedKarimul`
- Yousra Amin <sub> `Yousra-Amin`
- Muhtadina Serniabat Tasin <sub> `Muhtadina`
</br>

## Functional Requirements:
### 1. User Authentication and Authorization
- [ ]	**Registration:** `EMAIL` `PASSWORD` `CELL NUMBER` | _By default, users are marked as "unverified."_
- [ ]	**Login:** `email` `password`
- [ ]	 **Password Management:**
    -  change password 
    - recover password via email / phone number OTP
- [ ]	**Refresh Token:** refresh token mechanism to generate new access tokens
- [ ]	**Phone Number Verification:** verify by an `OTP` sent to phone number. | _No admin verification is required._
- [ ]	**Admin Ban:** preventing them from posting, commenting, voting

 
### 2. Crime Reporting
- [ ] **Report Crime:**
  - Only verified users can report crimes. </br>
  - Users must **upload at least one image** of the crime scene (video is optional). </br>
  - Users must **select the division + district** of the crime (use a free API or a predefined list of Bangladesh divisions and districts). </br>
  - **auto-generate a description** of the crime scene using an AI, based on the **uploaded image**. _Users can modify the description before posting_.</br>
  - If a video is uploaded, no AI-generated description will be provided. The user must manually add a description.

- [ ]	**Crime Post:**
  - Title (user-defined)
  - Description (AI-generated for images and user-editable; manually added for videos)
  - Division + district.
  - Image(s) and optional video.
  - Post Time: Timestamp of the post 
  - Crime Time: Timestamp the crime occurrence (user-defined).


### 3. Community Interaction
- [ ]	**Upvote/Downvote 
- [ ]	**Comments with Proof:** comment on crime posts - add additional proof (mandatory)
- [ ]	**Post Verification Score:** score based on upvotes, downvotes, verified comments.


### 4. Crime Feed
-	`PAGINATION`: Display crime posts …
-	`FILTERING` by division, district, verification score.
-	`SORTING`: by date, upvotes, verification score.
-	`SEARCHING`: Users can search for posts by keywords in the title or description.

 
### 5. User Roles
  - Unverified User:
    - Can view crime posts.
    - Cannot post crimes, comment, upvote, or downvote.

  -	Verified User:
    -	Can post crimes, comment, upvote, and downvote.

  -	Admin:
    - `spectate` all posts, users, comments
    - `remove` posts / comments
    - `ban user` 


### 6. User Profile
- [ ]	profile page showcasing details.
- [ ]	Profile Image: Users must upload a profile picture, which will be displayed on their profile and in their interactions (posts, comments).
- [ ]	Crime Reports: Displays a list of crime reports filed by the user, including details like report title, location, and date.
- [ ]	Other Information: Additional fields such as bio and contact information (optional).
- [ ]	Edit Profile: Users can update their profile picture, bio, and other details through an edit option.


<!--
Non-Functional Requirements:
1.	Security:
  - Hash passwords using a secure algorithm (e.g., bcrypt).
  - Use JWT for authentication and authorization.
  - Implement security best practices to protect against common vulnerabilities (e.g., SQL injection, XSS, CSRF).

2.	Responsive Design: The application should be mobile-friendly and responsive.
-->

 
## Technical Requirements (Technology-Agnostic):
### 1. Frontend:
  - Framework: React, Angular, Vue.js, Svelte, or plain HTML/CSS/JavaScript
  - Styling: CSS framework or custom styling : Tailwind CSS, Bootstrap, Material-UI, or SCSS
  - State Management: Optional, depending on the framework (e.g., Redux for React, Vuex for Vue.js, or built-in state management tools).

### 2. Backend:
  - Framework: Node.js with Express, Django, Flask, Spring Boot, Ruby on Rails, or Laravel
  - Database: MongoDB, PostgreSQL, MySQL, Firebase, or SQLite
  - File Storage: AWS S3, Firebase Storage, min.io

### 3. AI Integration:
  - AI tool / API : OpenAI's GPT / Google Vision API / custom machine learning models

### 4. APIs:
  - OTP : FIREBASE / NEXMO / local provider

### 5. Hosting (Bonus Feature):
  - Frontend: Netlif / Vercel / GitHub Pages / Firebase Hosting
  - Backend: Heroku / AWS / DigitalOcean / Render
  - Database: any cloud database service / self-hosted database

<!--
Additional Features:
1.	Heatmap: Display a heatmap of crime reports based on location.
2.	Leader board: Show top contributors (users with the most posts or helpful comments).
-->
