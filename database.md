-- 1. User Table
CREATE TABLE `User` (
    user_id CHAR(36) PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    phone VARCHAR(20) UNIQUE NOT NULL,
    is_verified BOOLEAN DEFAULT FALSE,
    is_banned BOOLEAN DEFAULT FALSE
);

-- 2. Division Table (Predefined Bangladesh divisions)
CREATE TABLE Division (
    division_id CHAR(36) PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 3. District Table (Predefined Bangladesh districts)
CREATE TABLE District (
    district_id CHAR(36) PRIMARY KEY,
    division_id CHAR(36) NOT NULL,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE (division_id, name),
    FOREIGN KEY (division_id) REFERENCES Division(division_id) ON DELETE CASCADE
);

-- 4. CrimePost Table
CREATE TABLE CrimePost (
    post_id CHAR(36) PRIMARY KEY,
    user_id CHAR(36) NOT NULL,
    title VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    division_id CHAR(36) NOT NULL,
    district_id CHAR(36) NOT NULL,
    crime_time TIMESTAMP NOT NULL,
    post_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    verification_score INT DEFAULT 0,
    FOREIGN KEY (user_id) REFERENCES `User`(user_id) ON DELETE CASCADE,
    FOREIGN KEY (division_id) REFERENCES Division(division_id) ON DELETE CASCADE,
    FOREIGN KEY (district_id) REFERENCES District(district_id) ON DELETE CASCADE
);

-- 5. Comment Table (Moved up to avoid FK issue in Media)
CREATE TABLE Comment (
    comment_id CHAR(36) PRIMARY KEY,
    user_id CHAR(36) NOT NULL,
    post_id CHAR(36) NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES `User`(user_id) ON DELETE CASCADE,
    FOREIGN KEY (post_id) REFERENCES CrimePost(post_id) ON DELETE CASCADE
);

-- 6. Media Table (Handles both posts and comments)
CREATE TABLE Media (
    media_id CHAR(36) PRIMARY KEY,
    post_id CHAR(36),
    comment_id CHAR(36),
    file_path VARCHAR(255) NOT NULL,
    media_type VARCHAR(10) CHECK (media_type IN ('image', 'video')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CHECK (post_id IS NOT NULL OR comment_id IS NOT NULL),
    FOREIGN KEY (post_id) REFERENCES CrimePost(post_id) ON DELETE CASCADE,
    FOREIGN KEY (comment_id) REFERENCES Comment(comment_id) ON DELETE CASCADE
);

-- 7. Vote Table
CREATE TABLE Vote (
    vote_id CHAR(36) PRIMARY KEY,
    user_id CHAR(36) NOT NULL,
    post_id CHAR(36) NOT NULL,
    vote_type VARCHAR(4) CHECK (vote_type IN ('up', 'down')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE (user_id, post_id),
    FOREIGN KEY (user_id) REFERENCES `User`(user_id) ON DELETE CASCADE,
    FOREIGN KEY (post_id) REFERENCES CrimePost(post_id) ON DELETE CASCADE
);

-- 8. Password Reset Table
CREATE TABLE PasswordReset (
    reset_id CHAR(36) PRIMARY KEY,
    user_id CHAR(36) NOT NULL,
    expires_at TIMESTAMP NOT NULL CHECK (expires_at > CURRENT_TIMESTAMP),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES `User`(user_id) ON DELETE CASCADE
);

-- 9. User Profile Table
CREATE TABLE UserProfile (
    profile_id CHAR(36) PRIMARY KEY,
    user_id CHAR(36) UNIQUE NOT NULL,
    profile_image_path VARCHAR(255) DEFAULT 'default_profile.png',
    bio TEXT,
    contact_info TEXT,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES `User`(user_id) ON DELETE CASCADE
);
