# Sync-TOD-SQL-Level


/*SYNC ATB02 LEVEL SQL*/

/*Fungsi keperluan transasaksi*/

USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetShiftID] (@shift int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @shift_id as  varchar(50);
SELECT @shift_id=(select id from _toll_shifts where nama = CAST(@shift AS varchar(1)));
 return @shift_id;
END;

GO


USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetPultolID] (@pultol int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @pultol_id as  varchar(50);
SELECT @pultol_id=(select id from _toll_employee where empid = @pultol);
 return @pultol_id;
END;

GO


USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetPengawasID] (@pengawas int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @pengawas_id as  varchar(50);
SELECT @pengawas_id=(select id from _toll_employee where empid = @pengawas);
 return @pengawas_id;
END;

GO


USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetBoothID] (@gid int,@gb int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @booth_id as  varchar(50);
SELECT @booth_id=(select id from _toll_booths where gid = @gid and gbid = 'GB0' + CAST(@gb AS varchar(1)));
 return @booth_id;
END;

GO


USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetGateID] (@gb int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @gate_id as  varchar(50);
SELECT @gate_id=(select id from _toll_gates where urutan = @gb);
 return @gate_id;
END;

GO

USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetClassID] (@URUTAN int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @class_id as  varchar(50);
SELECT @class_id=(select tc.id from _toll_classes  tc
	where tc.urutan=@URUTAN);
 return @class_id;
END;

GO



USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetBoothtaskID] (@perioda_id varchar(50))
RETURNS varchar(50)
 AS
BEGIN
DECLARE @boothtask_id as  varchar(50);
SELECT @boothtask_id=(select tb.id from _toll_boothtasks  tb
	where tb.perioda_id=@perioda_id);
 return @boothtask_id;
END;

GO


USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetBoothtaskShiftID] (@date date, @shift_id varchar(50),@pultol_id varchar(50),@pengawas_id varchar(50),@report_type_id int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @boothtask_shift_id as  varchar(50);
SELECT @boothtask_shift_id=(SELECT tbs.id from _toll_boothtask_shift tbs 
where CONVERT(date, tbs.date)=CONVERT(date, @date) and tbs.shift_id=@shift_id and 
tbs.pultol_id=@pultol_id and tbs.pengawas_id=@pengawas_id and tbs.report_type_id=@report_type_id);
 return @boothtask_shift_id;
END;

GO



USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetPaymentID] (@URUTAN int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @payment_id as  varchar(50);
SELECT @payment_id=(select tp.id from _toll_payments  tp
	where tp.urutan=@URUTAN);
 return @payment_id;
END;

GO

 

USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetTicketID] (@tiket int,@tonase int)
RETURNS varchar(50)
 AS
BEGIN
DECLARE @TICKETIDRES as  varchar(50);
DECLARE @TICKETID as  varchar(5);

SELECT @TICKETID=
(SELECT CASE 
            WHEN @tiket = 0 or @tiket = 1
               THEN 'P12'
					WHEN @tiket = 4 or @tiket = 5
					   THEN 'P01'
						   WHEN @tiket = 7 and @tonase = 0
						   THEN 'P07'
							   WHEN @tiket = 7 and (@tonase = 1 or @tonase = 2)
							   THEN 'P06'
								   WHEN @tiket = 2
								   THEN 'P02'
       END)


SELECT @TICKETIDRES=(select tt.id from _toll_tickets   tt
	where tt.ticket_id=@TICKETID);
 return @TICKETIDRES;
END;

GO

 

USE [MIS]
GO

/****** Object:  UserDefinedFunction [dbo].[fnGetRelevance]    Script Date: 07/04/2016 10:58:44 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[fOPGetFarerampID] (@tarifid int,@class_id varchar(50),@ticket_id varchar(50),@gate varchar(50))
RETURNS varchar(50)
 AS
BEGIN 
DECLARE @fares_id as  varchar(50);
DECLARE @fareramp_id as  varchar(50);
SELECT @fares_id=(select tf.id from _toll_fares  tf
	where tf.tarif_id=@tarifid);
SELECT @fareramp_id=(select tfm.id from _toll_faresramp  tfm
	where tfm.fare_id=@fares_id and tfm.classes_id=@class_id and tfm.ticket_id=@ticket_id and tfm.gate=@gate);
 return @fareramp_id;
END;

GO




CREATE PROCEDURE dbo.uspSyncATB02
AS

insert into [MIS].[dbo].[_toll_boothtask_shift]
select * from (
select top 10
newid() id,CAST(tp.dt_tutup as datetime) as date
		,dbo.[fOPGetShiftID](tp.shift) shift_id,dbo.[fOPGetPultolID](tp.pultol_id) pultol_id, dbo.[fOPGetPengawasID](tp.pengawas_buka_id) pengawas_id, null am_id,null document_id,tp.operasi report_type_id,
		dbo.[fOPGetGateID](tp.gb) gate_id,dbo.[fOPGetBoothID](tp.gid, tp.gb) booth_id,tp.status
from t_perioda tp
where tp.status=1 and tp.operasi=2 and tp.pengawas_buka_id!=99
group by CAST(tp.dt_tutup as datetime),DATEPART(hour,tp.dt_tutup),tp.shift,tp.pultol_id,tp.pengawas_buka_id,tp.operasi,tp.status,tp.gb,tp.gid
order by CAST(tp.dt_tutup as datetime) desc, DATEPART(hour,tp.dt_tutup) desc ) tmp
where NOT EXISTS (SELECT * from _toll_boothtask_shift tbs 
where CONVERT(date, tbs.date)=CONVERT(date, tmp.date) and tbs.shift_id=tmp.shift_id and 
tbs.pultol_id=tmp.pultol_id and tbs.pengawas_id=tmp.pengawas_id and tbs.report_type_id=tmp.report_type_id )

insert into [MIS].[dbo].[_toll_boothtasks]
select tmp.id,tmp.report_date,tmp.gate_id,tmp.report_type_id,tmp.booth_id,tmp.status_id,
tmp.pultol_id,tmp.shift_id,tmp.pengawas_id,tmp.perioda_id,
GETDATE() createddate, GETDATE() dateupdated, null datedeleted,tmp.perioda_no,
[dbo].[fOPGetBoothtaskShiftID] (tmp.report_date, tmp.shift_id,tmp.pultol_id,tmp.pengawas_id,tmp.report_type_id) bothtaskshift_id,
tmp.open_date,tmp.close_date
 from (
select top 10 NEWID() id, tp.dt_report report_date,dbo.[fOPGetGateID](tp.gb) gate_id,
tp.operasi report_type_id, dbo.[fOPGetBoothID](tp.gid, tp.gb) booth_id,
tp.status status_id, dbo.[fOPGetPultolID](tp.pultol_id) pultol_id,
dbo.[fOPGetShiftID](tp.shift) shift_id,
dbo.[fOPGetPengawasID](tp.pengawas_buka_id) pengawas_id,
tp.id perioda_id,  tp.periode_no perioda_no,
tp.dt_buka open_date, tp.dt_tutup close_date
from t_perioda tp
where tp.status=1 and tp.operasi=2
order by tp.dt_tutup desc ) tmp
where NOT EXISTS (SELECT * from _toll_boothtasks tb
where tb.perioda_id=tmp.perioda_id )

insert into [MIS].[dbo].[_toll_opensystemtransaction]
select * from (
select NEWID() id,[dbo].[fOPGetBoothtaskID](tmp.perioda_id) boothtask_id,null transaction_type_id
,dbo.[fOPGetClassID](tmp.golongan) class_id,null card_type_id,
tmp.origin1 traffic_counter,null traffic_type, tmp.trans_type transtype, dbo.[fOPGetTicketID](tmp.tiket,tmp.tonase) ticked_id,
dbo.[fOPGetPaymentID](tmp.pembayaran) payment_id,null transtypekdbayar_id, 
[dbo].[fOPGetFarerampID](tmp.tarif_id,dbo.[fOPGetClassID](tmp.golongan),dbo.[fOPGetTicketID](tmp.tiket,tmp.tonase),[dbo].[fOPGetGateID](tmp.gb)) fareramp_id,
null gate_origin_id,null transaction_id
  from (
select top 100 tp.id perioda_id,tp.tarif_id,tp.gb, (tpl.trans_type%8) golongan, ((tpl.trans_type/16)%8) tiket, 
((tpl.trans_type/128)%8) pembayaran, 
CASE WHEN ((tpl.trans_type/1024)%8)=0 THEN 8 ELSE ((tpl.trans_type/1024)%8) END tonase,
	 tpl.trans_type, tpl.origin1
from t_perioda_lalin tpl left join t_perioda tp on tpl.periode_id=tp.id
where tp.status=1 and tp.operasi=2
order by tp.dt_tutup desc ) tmp ) tmp2
where NOT EXISTS (SELECT * from _toll_opensystemtransaction tpe
where tpe.boothtask_id=tmp2.boothtask_id and tpe.transtype=tmp2.transtype )

GO

exec dbo.uspSyncATB02

/*Jalankan SP dbo.uspSyncATB02 menggunakan job sql server agent pada jam tutup shift (6-7, 14-15, 22-23) setiap 3 menit sekali*/

