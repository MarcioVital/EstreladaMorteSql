# EstreladaMorteSql
Projeto realizado em SQL Sever

Apredendo mais um pouquinho!


USE [EstrelaDaMorte]
GO
/****** Object:  Table [dbo].[HistoricoViagens]    Script Date: 13/10/2021 20:33:49 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[HistoricoViagens](
	[IdNave] [int] NOT NULL,
	[IdPiloto] [int] NOT NULL,
	[DtSaida] [datetime] NOT NULL,
	[DtChegada] [datetime] NULL
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Naves]    Script Date: 13/10/2021 20:33:49 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Naves](
	[IdNave] [int] NOT NULL,
	[Nome] [varchar](50) NOT NULL,
	[Modelo] [varchar](50) NOT NULL,
	[Passageiro] [int] NOT NULL,
	[Carga] [float] NOT NULL,
	[Classe] [varchar](50) NOT NULL,
 CONSTRAINT [PK_Naves] PRIMARY KEY CLUSTERED 
(
	[IdNave] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Pilotos]    Script Date: 13/10/2021 20:33:49 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Pilotos](
	[IdPiloto] [int] NOT NULL,
	[Nome] [varchar](50) NOT NULL,
	[AnoNascimento] [varchar](10) NOT NULL,
	[IdPlaneta] [int] NOT NULL,
 CONSTRAINT [PK_Pilotos] PRIMARY KEY CLUSTERED 
(
	[IdPiloto] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[PilotosNaves]    Script Date: 13/10/2021 20:33:49 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[PilotosNaves](
	[IdPiloto] [int] NOT NULL,
	[IdNave] [int] NOT NULL,
	[FlagAutorizado] [bit] NOT NULL,
 CONSTRAINT [Pk_PilotosNaves] PRIMARY KEY CLUSTERED 
(
	[IdPiloto] ASC,
	[IdNave] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Planetas]    Script Date: 13/10/2021 20:33:49 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Planetas](
	[IdPlaneta] [int] NOT NULL,
	[Nome] [varchar](50) NOT NULL,
	[Rotacao] [float] NOT NULL,
	[Horbita] [float] NOT NULL,
	[Diametro] [float] NOT NULL,
	[Clima] [varchar](50) NOT NULL,
	[Populacao] [int] NOT NULL,
 CONSTRAINT [PK_Planetas] PRIMARY KEY CLUSTERED 
(
	[IdPlaneta] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
ALTER TABLE [dbo].[PilotosNaves] ADD  CONSTRAINT [DF_PilotosNaves_FlagAutorizado]  DEFAULT ((1)) FOR [FlagAutorizado]
GO
ALTER TABLE [dbo].[HistoricoViagens]  WITH CHECK ADD  CONSTRAINT [FK_HistoricoViagens_PilotosNaves] FOREIGN KEY([IdPiloto], [IdNave])
REFERENCES [dbo].[PilotosNaves] ([IdPiloto], [IdNave])
GO
ALTER TABLE [dbo].[HistoricoViagens] CHECK CONSTRAINT [FK_HistoricoViagens_PilotosNaves]
GO
ALTER TABLE [dbo].[Pilotos]  WITH CHECK ADD  CONSTRAINT [FK_Pilotos_Planetas] FOREIGN KEY([IdPlaneta])
REFERENCES [dbo].[Planetas] ([IdPlaneta])
GO
ALTER TABLE [dbo].[Pilotos] CHECK CONSTRAINT [FK_Pilotos_Planetas]
GO
ALTER TABLE [dbo].[PilotosNaves]  WITH CHECK ADD  CONSTRAINT [FK_PilotosNaves_Naves] FOREIGN KEY([IdNave])
REFERENCES [dbo].[Naves] ([IdNave])
GO
ALTER TABLE [dbo].[PilotosNaves] CHECK CONSTRAINT [FK_PilotosNaves_Naves]
GO
ALTER TABLE [dbo].[PilotosNaves]  WITH CHECK ADD  CONSTRAINT [FK_PilotosNaves_Pilotos] FOREIGN KEY([IdPiloto])
REFERENCES [dbo].[Pilotos] ([IdPiloto])
GO
ALTER TABLE [dbo].[PilotosNaves] CHECK CONSTRAINT [FK_PilotosNaves_Pilotos]
GO
