# last
##系统分层结构图
![default](https://user-images.githubusercontent.com/16076963/28245170-162903b4-6a33-11e7-8492-231ce5086151.png)

##删除教师
![default](https://user-images.githubusercontent.com/16076963/28245204-0b0aaaf4-6a34-11e7-8933-cb5facc7cf46.png)
##修改教师信息
![default](https://user-images.githubusercontent.com/16076963/28245416-cdfbe4f2-6a38-11e7-8bb0-d03d8d7b23ea.png)
##新增教师
![default](https://user-images.githubusercontent.com/16076963/28245233-dbcc145c-6a34-11e7-9cef-e2f0dc73f4ff.png)
##选了某门课程的人
![default](https://user-images.githubusercontent.com/16076963/28245250-34659976-6a35-11e7-90b6-e2922ffe0d42.png)
##新增排课

##删除课程
![default](https://user-images.githubusercontent.com/16076963/28245306-2d61b6f4-6a36-11e7-816d-899953d79371.png)
##修改课程
![default](https://user-images.githubusercontent.com/16076963/28245330-9c9ce746-6a36-11e7-81e8-4e32f2e3a430.png)
##新增课程
![default](https://user-images.githubusercontent.com/16076963/28245338-d879bcb2-6a36-11e7-937d-76272f6787e6.png)
##查看成绩
![default](https://user-images.githubusercontent.com/16076963/28245426-f6dc811a-6a38-11e7-864c-862ed5801205.png)
##选了的课程
![default](https://user-images.githubusercontent.com/16076963/28245359-3e96d430-6a37-11e7-866f-1c03516bc736.png)
##已选该课程选课失败
![default](https://user-images.githubusercontent.com/16076963/28245433-1f6b2a8c-6a39-11e7-9ceb-48498854b775.png)
##未选先修课程
![default](https://user-images.githubusercontent.com/16076963/28245441-45ef319e-6a39-11e7-9ac2-788cf1eea638.png)
##选课成功
![default](https://user-images.githubusercontent.com/16076963/28245385-046bc134-6a38-11e7-8e68-c3231ee24a47.png)
##主页
![default](https://user-images.githubusercontent.com/16076963/28245446-66bb5e7a-6a39-11e7-8a08-d04222bc5f98.png)
##登录
[default](https://user-images.githubusercontent.com/16076963/28245392-3d2041bc-6a38-11e7-939f-f0f5a2959558.png)
##UML
![uml](https://user-images.githubusercontent.com/16076963/28245398-605d97ba-6a38-11e7-98d6-92eede7f297e.png)
#数据库
/*
Navicat SQLite Data Transfer

Source Server         : 111
Source Server Version : 30714
Source Host           : :0

Target Server Type    : SQLite
Target Server Version : 30714
File Encoding         : 65001

Date: 2017-07-01 17:46:26
*/

PRAGMA foreign_keys = OFF;

-- ----------------------------
-- Table structure for Course
-- ----------------------------
DROP TABLE IF EXISTS "main"."Course";
CREATE TABLE [Course] (
[courseNo] VARCHAR(20)  PRIMARY KEY NOT NULL,
[courseName] VARCHAR(30)  NULL,
[credits] FLOAT  NULL
);

-- ----------------------------
-- Records of Course
-- ----------------------------
INSERT INTO "main"."Course" VALUES ('JAVA01', 'Java1', 3.0);
INSERT INTO "main"."Course" VALUES ('JAVA02', 'Java2', 3.0);
INSERT INTO "main"."Course" VALUES ('GLX01', '管理学', 3.0);
INSERT INTO "main"."Course" VALUES ('XTFX', '系统分析', 3.5);
INSERT INTO "main"."Course" VALUES ('WEB01', '网页设计', 4.0);

-- ----------------------------
-- Table structure for Course_prerequisites
-- ----------------------------
DROP TABLE IF EXISTS "main"."Course_prerequisites";
CREATE TABLE [Course_prerequisites] (
[PrerequisitesNo] VARCHAR(20)  NOT NULL,
[courseNo] VARCHAR(20)  NULL
);

-- ----------------------------
-- Records of Course_prerequisites
-- ----------------------------
INSERT INTO "main"."Course_prerequisites" VALUES ('JAVA01', 'JAVA02');
INSERT INTO "main"."Course_prerequisites" VALUES ('WEB01', 'XTFX');

-- ----------------------------
-- Table structure for Professor
-- ----------------------------
DROP TABLE IF EXISTS "main"."Professor";
CREATE TABLE [Professor] (
[PSsn] VARCHAR(20)  PRIMARY KEY NULL,
[name] VARCHAR(30)  NULL,
[password] VARCHAR(20)  NULL,
[title] VARCHAR(20)  NULL,
[department] VARCHAR(30)  NULL
);

-- ----------------------------
-- Records of Professor
-- ----------------------------
INSERT INTO "main"."Professor" VALUES (123, '杨明智', 123, '讲师', '管院');
INSERT INTO "main"."Professor" VALUES (456, '王辉', 456, '副教授', '管院');
INSERT INTO "main"."Professor" VALUES (789, '张卫华', 789, '教授', '管院');

-- ----------------------------
-- Table structure for ScheduleOfClasses
-- ----------------------------
DROP TABLE IF EXISTS "main"."ScheduleOfClasses";
CREATE TABLE [ScheduleOfClasses](
    [semester] VARCHAR(20), 
    [sectionNo] INTEGER REFERENCES Section([sectionNo]));

-- ----------------------------
-- Records of ScheduleOfClasses
-- ----------------------------
INSERT INTO "main"."ScheduleOfClasses" VALUES (201501, 1);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201501, 2);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201501, 3);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201501, 4);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201502, 3);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201502, 4);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201502, 5);
INSERT INTO "main"."ScheduleOfClasses" VALUES (201501, 5);

-- ----------------------------
-- Table structure for Section
-- ----------------------------
DROP TABLE IF EXISTS "main"."Section";
CREATE TABLE [Section](
    [sectionNo] INTEGER PRIMARY KEY NOT NULL REFERENCES ScheduleOfClasses([sectionNo]), 
    [dayOfWeek] VARCHAR(10), 
    [timeOfDay] VARCHAR(20), 
    [room] VARCHAR(20), 
    [seatingCapacity] INTEGER, 
    [courseNo] VARCHAR(20), 
    [PSsn] VARCHAR(20));

-- ----------------------------
-- Records of Section
-- ----------------------------
INSERT INTO "main"."Section" VALUES (1, '周一', '8:10-10:00 AM', 'J1B101', 75, 'JAVA01', 123);
INSERT INTO "main"."Section" VALUES (2, '周二', '6:10-8:00 PM', 'J1B102', 70, 'JAVA02', 456);
INSERT INTO "main"."Section" VALUES (3, '周三', '8:10-10:00 AM', 'J1B103', 68, 'GLX01', 456);
INSERT INTO "main"."Section" VALUES (4, '周四', '10:10-12:00 AM', 'J1B201', 75, 'XTFX', 123);
INSERT INTO "main"."Section" VALUES (5, '周五', '8:10-10:00 AM', 'J1B202', 75, 'WEB01', 789);

-- ----------------------------
-- Table structure for sqlite_sequence
-- ----------------------------
DROP TABLE IF EXISTS "main"."sqlite_sequence";
CREATE TABLE sqlite_sequence(name,seq);

-- ----------------------------
-- Records of sqlite_sequence
-- ----------------------------
INSERT INTO "main"."sqlite_sequence" VALUES ('Transcript', 44);

-- ----------------------------
-- Table structure for Student
-- ----------------------------
DROP TABLE IF EXISTS "main"."Student";
CREATE TABLE [Student] (
[SSsn] VARCHAR(20)  PRIMARY KEY NULL,
[name] VARCHAR(30)  NULL,
[password] VARCHAR(20)  NULL,
[major] VARCHAR(30)  NULL,
[degree] VARCHAR(20)  NULL
);

-- ----------------------------
-- Records of Student
-- ----------------------------
INSERT INTO "main"."Student" VALUES ('09143001', '杨木', 123, '电商', '学士');
INSERT INTO "main"."Student" VALUES ('09143002', '李杨', 456, '电商', '学士');
INSERT INTO "main"."Student" VALUES ('09143003', '马云', 789, '电商', '学士');

-- ----------------------------
-- Table structure for Transcript
-- ----------------------------
DROP TABLE IF EXISTS "main"."Transcript";
CREATE TABLE [Transcript](
    [transcriptNo] INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, 
    [SSsn] VARCHAR(20) REFERENCES Student([SSsn]), 
    [sectionNo] INTEGER, 
    [grade] VARCHAR(10));

-- ----------------------------
-- Records of Transcript
-- ----------------------------
INSERT INTO "main"."Transcript" VALUES (35, '09143002', 1, 80);
INSERT INTO "main"."Transcript" VALUES (42, '09143003', 3, 85);


