# KP72_Arnautova_Anna_DB1
Лабораторна робота № 1.

Ознайомлення з базовими операціями СУБД PostgreSQL

КП-72 Арнаутова Ганна Сергіївна

Варіант 2 - Готель

Сутності:

1. Гість (Guest)
CREATE TABLE public."Guests"
(
    id integer NOT NULL DEFAULT nextval('"Guests_id_seq"'::regclass),
    "Name" text COLLATE pg_catalog."default" NOT NULL,
    "Surname" text COLLATE pg_catalog."default" NOT NULL,
    "StatusId" integer NOT NULL DEFAULT nextval('"Guests_StatusId_seq"'::regclass),
    CONSTRAINT "Guests_pkey" PRIMARY KEY (id),
    CONSTRAINT "StatusId_fk" FOREIGN KEY ("StatusId")
        REFERENCES public."GuestStatus" (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

2. Статус (GuestStatus)
CREATE TABLE public."GuestStatus"
(
    id integer NOT NULL DEFAULT nextval('"GuestStatus_id_seq"'::regclass),
    "StatusName" text COLLATE pg_catalog."default" NOT NULL,
    "RequiredVisits" smallint NOT NULL,
    CONSTRAINT "GuestStatus_pkey" PRIMARY KEY (id)
)

3. Кімната (Room)
CREATE TABLE public."Rooms"
(
    id integer NOT NULL DEFAULT nextval('"Rooms_id_seq"'::regclass),
    "TypeId" integer NOT NULL DEFAULT nextval('"Rooms_TypeId_seq"'::regclass),
    "Number" text COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT "Rooms_pkey" PRIMARY KEY (id),
    CONSTRAINT "TypeId_fk" FOREIGN KEY ("TypeId")
        REFERENCES public."RoomType" (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

4. Тип кімнати (RoomType)
CREATE TABLE public."RoomType"
(
    id integer NOT NULL DEFAULT nextval('"RoomType_id_seq"'::regclass),
    "TypeName" text COLLATE pg_catalog."default" NOT NULL,
    "BedCount" smallint NOT NULL,
    "Price" money,
    CONSTRAINT "RoomType_pkey" PRIMARY KEY (id)
)

5. Бронь (Booking)
REATE TABLE public."Booking"
(
    id integer NOT NULL DEFAULT nextval('"Booking_id_seq"'::regclass),
    "GuestId" integer NOT NULL DEFAULT nextval('"Booking_GuestId_seq"'::regclass),
    "RoomId" integer NOT NULL DEFAULT nextval('"Booking_RoomId_seq"'::regclass),
    "Arrive" date NOT NULL,
    "Departure" date NOT NULL,
    "Sum" money NOT NULL,
    CONSTRAINT "Booking_pkey" PRIMARY KEY (id),
    CONSTRAINT "GuestId_fk" FOREIGN KEY ("GuestId")
        REFERENCES public."Guests" (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT "RoomId_fk" FOREIGN KEY ("RoomId")
        REFERENCES public."Rooms" (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)
