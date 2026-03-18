This is the Sql code for XAMPP DataBase 



-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1
-- Generation Time: Dec 10, 2025 at 02:54 AM
-- Server version: 10.4.32-MariaDB
-- PHP Version: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `campus_connect`
--

-- --------------------------------------------------------

--
-- Table structure for table `activity_logs`
--

CREATE TABLE `activity_logs` (
  `log_id` int(11) NOT NULL,
  `user_id` int(11) NOT NULL,
  `action` varchar(50) NOT NULL,
  `timestamp` datetime NOT NULL DEFAULT current_timestamp(),
  `logout_time` datetime DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `activity_logs`
--

INSERT INTO `activity_logs` (`log_id`, `user_id`, `action`, `timestamp`, `logout_time`) VALUES
(58, 8, 'Login', '2025-12-05 00:20:35', '2025-12-05 00:20:49'),
(59, 14, 'Login', '2025-12-05 00:20:57', '2025-12-05 00:21:09'),
(60, 8, 'Login', '2025-12-05 00:21:14', '2025-12-05 00:21:36'),
(61, 14, 'Login', '2025-12-05 00:21:45', '2025-12-05 00:44:10'),
(62, 8, 'Login', '2025-12-05 00:44:16', NULL);

-- --------------------------------------------------------

--
-- Table structure for table `anonymousmessages`
--

CREATE TABLE `anonymousmessages` (
  `message_id` int(11) NOT NULL,
  `message_text` text NOT NULL,
  `tags` varchar(255) DEFAULT NULL,
  `attachment_link` varchar(255) DEFAULT NULL,
  `ip_address` varchar(45) DEFAULT NULL,
  `created_at` datetime NOT NULL DEFAULT current_timestamp(),
  `is_read` tinyint(1) DEFAULT 0,
  `is_favorite` tinyint(1) DEFAULT 0,
  `is_archived` tinyint(1) DEFAULT 0,
  `is_reviewed` tinyint(1) DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `anonymousmessages`
--

INSERT INTO `anonymousmessages` (`message_id`, `message_text`, `tags`, `attachment_link`, `ip_address`, `created_at`, `is_read`, `is_favorite`, `is_archived`, `is_reviewed`) VALUES
(25, 'read', '', NULL, '::1', '2025-12-03 22:59:24', 0, 0, 0, 1),
(26, 'favorite', '', NULL, '::1', '2025-12-03 22:59:36', 1, 0, 0, 0),
(27, 'archived', '', NULL, '::1', '2025-12-03 22:59:52', 0, 1, 0, 0),
(28, 'reviewed', '', NULL, '::1', '2025-12-03 23:00:05', 0, 1, 0, 0),
(29, 'hiiii', '', NULL, '::1', '2025-12-04 11:07:26', 0, 0, 0, 0),
(30, 'hiii', '', NULL, '::1', '2025-12-04 11:30:51', 0, 0, 0, 0),
(31, 'asda', '', NULL, '::1', '2025-12-04 11:31:12', 0, 0, 0, 0),
(32, 'asdas', '', NULL, '::1', '2025-12-04 11:31:15', 1, 0, 0, 0),
(33, 'd', '', NULL, '::1', '2025-12-04 11:35:49', 0, 1, 0, 0),
(34, 's', '', NULL, '::1', '2025-12-04 11:35:52', 0, 0, 0, 1),
(35, 'ds', '', NULL, '::1', '2025-12-04 11:35:54', 0, 0, 1, 0),
(36, 'dad', '', NULL, '::1', '2025-12-04 11:35:57', 0, 1, 0, 0),
(37, 'dssad', '', NULL, '::1', '2025-12-04 11:36:00', 1, 0, 0, 0),
(38, 'asdas', '', NULL, '::1', '2025-12-04 11:40:42', 0, 1, 0, 0),
(39, 'gwapo ko', '', '1764826318_0_IMG_8233.JPG,1764826318_1_IMG_8234.JPG,1764826318_2_IMG_8251.JPG,1764826318_3_IMG_8253.JPG', '::1', '2025-12-04 13:31:58', 0, 0, 0, 0),
(40, 'adsas #Complaint ', 'Complaint', NULL, '::1', '2025-12-04 16:58:28', 0, 0, 0, 0),
(41, 'asdaasa #Concern ', 'Concern', NULL, '::1', '2025-12-04 16:58:33', 0, 0, 0, 0),
(42, 'dadsw #Query ', 'Query', NULL, '::1', '2025-12-04 16:58:38', 1, 0, 0, 0),
(43, 'kuan #Complaint ', 'Complaint', NULL, '::1', '2025-12-04 18:31:08', 0, 0, 0, 0),
(44, 'bayottt', '', NULL, '::1', '2025-12-04 19:16:54', 0, 0, 0, 0),
(45, 'bayott', '', NULL, '::1', '2025-12-04 19:17:02', 0, 0, 0, 0),
(46, 'okay kayow', '', NULL, '::1', '2025-12-04 19:47:32', 0, 0, 0, 0),
(47, 'kwee #Concern #Complaint #Query ', 'Concern,Complaint,Query', NULL, '::1', '2025-12-04 19:47:56', 0, 0, 0, 0),
(48, 'Goodmorning', '', NULL, '::1', '2025-12-05 00:27:52', 0, 0, 0, 0);

--
-- Triggers `anonymousmessages`
--
DELIMITER $$
CREATE TRIGGER `trg_sync_anonymous_read_status` AFTER UPDATE ON `anonymousmessages` FOR EACH ROW BEGIN
    -- This trigger now updates the notifications based on the new structural link (anonymous_message_id)
    IF OLD.is_read <> NEW.is_read THEN
        UPDATE notifications
        SET is_read = NEW.is_read
        WHERE anonymous_message_id = NEW.message_id
        LIMIT 1;
    END IF;
END
$$
DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `events`
--

CREATE TABLE `events` (
  `event_id` int(11) NOT NULL,
  `user_id` int(11) DEFAULT NULL,
  `event_date` date NOT NULL,
  `title` varchar(255) NOT NULL,
  `description` text DEFAULT NULL,
  `created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `events`
--

INSERT INTO `events` (`event_id`, `user_id`, `event_date`, `title`, `description`, `created_at`) VALUES
(7, 8, '2025-12-11', 'Pasko sa CTU', '', '2025-12-03 23:33:22'),
(8, 8, '2025-12-05', 'Project Presentation', '', '2025-12-04 05:55:09'),
(9, 8, '2025-12-09', 'okay', '', '2025-12-04 11:06:33'),
(10, 8, '2025-12-19', 'year end', '', '2025-12-04 11:29:41'),
(11, 8, '2025-12-20', 'Year end', '', '2025-12-04 11:30:36'),
(13, 8, '2025-12-25', 'Pasko', '', '2025-12-04 13:34:28'),
(15, 8, '2025-12-31', 'New Year', '', '2025-12-04 18:29:40');

-- --------------------------------------------------------

--
-- Table structure for table `notifications`
--

CREATE TABLE `notifications` (
  `id` int(11) NOT NULL,
  `type` enum('message','event') NOT NULL,
  `text` varchar(255) NOT NULL,
  `is_read` tinyint(1) DEFAULT 0,
  `created_at` datetime NOT NULL DEFAULT current_timestamp(),
  `user_id` int(11) DEFAULT NULL,
  `anonymous_message_id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `notifications`
--

INSERT INTO `notifications` (`id`, `type`, `text`, `is_read`, `created_at`, `user_id`, `anonymous_message_id`) VALUES
(1, 'event', 'A user added a new event!', 0, '2025-12-04 11:06:33', NULL, NULL),
(2, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:07:26', NULL, 29),
(3, 'event', 'Villegas Khyan Earl G. added event: year end', 0, '2025-12-04 11:29:41', 8, NULL),
(5, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:30:51', NULL, 30),
(6, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:31:12', NULL, 31),
(7, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:31:15', NULL, 32),
(8, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:35:49', NULL, 33),
(9, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:35:52', NULL, 34),
(10, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:35:54', NULL, 35),
(11, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:35:57', NULL, 36),
(12, 'message', 'You have a new unread post. Tap to navigate!', 0, '2025-12-04 11:36:00', NULL, 37),
(13, 'event', 'Villegas Khyan Earl G. added event: Kuan', 0, '2025-12-04 13:34:22', 8, NULL),
(14, 'event', 'Villegas Khyan Earl G. added event: Pasko', 0, '2025-12-04 13:34:28', 8, NULL),
(15, 'event', 'Villegas Khyan Earl G. added event: New Year', 0, '2025-12-04 13:34:43', 8, NULL);

-- --------------------------------------------------------

--
-- Table structure for table `passwordreset`
--

CREATE TABLE `passwordreset` (
  `id` int(11) NOT NULL,
  `user_email` varchar(100) NOT NULL,
  `otp_code` varchar(10) NOT NULL,
  `expires_at` datetime NOT NULL,
  `created_at` datetime NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- --------------------------------------------------------

--
-- Table structure for table `users`
--

CREATE TABLE `users` (
  `user_id` int(11) NOT NULL,
  `fullname` varchar(100) NOT NULL,
  `email` varchar(100) NOT NULL,
  `birthday` date DEFAULT NULL,
  `profile_pic` varchar(255) DEFAULT NULL,
  `password` varchar(255) NOT NULL,
  `position` varchar(100) NOT NULL,
  `role` enum('admin','officer') NOT NULL DEFAULT 'officer',
  `is_approved` tinyint(1) NOT NULL DEFAULT 0,
  `created_at` datetime NOT NULL DEFAULT current_timestamp(),
  `approved_at` datetime DEFAULT NULL,
  `last_login` datetime DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `users`
--

INSERT INTO `users` (`user_id`, `fullname`, `email`, `birthday`, `profile_pic`, `password`, `position`, `role`, `is_approved`, `created_at`, `approved_at`, `last_login`) VALUES
(8, 'Villegas Khyan Earl G.', 'villegaskhyanearl@gmail.com', '2005-04-20', '1764847134_pfp_Gemini_Generated_Image_tqt360tqt360tqt3.png', '$2y$10$RmqhANJStVb.kKPT5Ws6Xech5L4aFcBitJ2pxQ1ZuVxueP28Ht022', 'DOCUMENTATION OFFICER', 'admin', 1, '2025-12-04 05:58:10', '2025-12-04 20:20:03', '2025-12-05 00:44:16'),
(14, 'Machica, John Lester M.', 'laxusmachica@gmail.com', NULL, NULL, '$2y$10$75S3.pnRqqwsJJcEXZGRuOJB37NwU581dz7D63KwcDC2x1abgOZ2i', 'LOGISTICS COMMITTEE', 'admin', 1, '2025-12-04 22:24:10', '2025-12-04 22:25:17', '2025-12-05 00:21:45'),
(15, 'Villegas Khyan Earl G.', 'villegaskhyan@gmail.com', '2005-04-20', '1764861733_pfp_1000236119.jpg', '$2y$10$SvDe3364HQgmA.Nt7N7S4eHjzH6DtmKv7HBf8Qulr1idKzVbcEtcW', 'DOCUMENTATION OFFICER', 'officer', 1, '2025-12-04 22:30:06', '2025-12-04 23:20:48', '2025-12-05 00:18:59');

--
-- Indexes for dumped tables
--

--
-- Indexes for table `activity_logs`
--
ALTER TABLE `activity_logs`
  ADD PRIMARY KEY (`log_id`),
  ADD KEY `fk_activity_logs` (`user_id`);

--
-- Indexes for table `anonymousmessages`
--
ALTER TABLE `anonymousmessages`
  ADD PRIMARY KEY (`message_id`);

--
-- Indexes for table `events`
--
ALTER TABLE `events`
  ADD PRIMARY KEY (`event_id`),
  ADD KEY `fk_event_creator` (`user_id`);

--
-- Indexes for table `notifications`
--
ALTER TABLE `notifications`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fk_notif_users` (`user_id`),
  ADD KEY `fk_notif_message` (`anonymous_message_id`);

--
-- Indexes for table `passwordreset`
--
ALTER TABLE `passwordreset`
  ADD PRIMARY KEY (`id`),
  ADD KEY `user_email` (`user_email`);

--
-- Indexes for table `users`
--
ALTER TABLE `users`
  ADD PRIMARY KEY (`user_id`),
  ADD UNIQUE KEY `email` (`email`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `activity_logs`
--
ALTER TABLE `activity_logs`
  MODIFY `log_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=63;

--
-- AUTO_INCREMENT for table `anonymousmessages`
--
ALTER TABLE `anonymousmessages`
  MODIFY `message_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=49;

--
-- AUTO_INCREMENT for table `events`
--
ALTER TABLE `events`
  MODIFY `event_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=16;

--
-- AUTO_INCREMENT for table `notifications`
--
ALTER TABLE `notifications`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=16;

--
-- AUTO_INCREMENT for table `passwordreset`
--
ALTER TABLE `passwordreset`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=12;

--
-- AUTO_INCREMENT for table `users`
--
ALTER TABLE `users`
  MODIFY `user_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=16;

--
-- Constraints for dumped tables
--

--
-- Constraints for table `activity_logs`
--
ALTER TABLE `activity_logs`
  ADD CONSTRAINT `fk_activity_logs` FOREIGN KEY (`user_id`) REFERENCES `users` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Constraints for table `events`
--
ALTER TABLE `events`
  ADD CONSTRAINT `fk_event_creator` FOREIGN KEY (`user_id`) REFERENCES `users` (`user_id`) ON DELETE SET NULL ON UPDATE CASCADE;

--
-- Constraints for table `notifications`
--
ALTER TABLE `notifications`
  ADD CONSTRAINT `fk_notif_message` FOREIGN KEY (`anonymous_message_id`) REFERENCES `anonymousmessages` (`message_id`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `fk_notif_users` FOREIGN KEY (`user_id`) REFERENCES `users` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Constraints for table `passwordreset`
--
ALTER TABLE `passwordreset`
  ADD CONSTRAINT `passwordreset_ibfk_1` FOREIGN KEY (`user_email`) REFERENCES `users` (`email`);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
