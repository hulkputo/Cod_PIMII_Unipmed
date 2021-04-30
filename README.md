# Cod_PIMII_Unipmed
using System;
using System.IO;
using System.Security.Cryptography;
using System.Text;
using iTextSharp.text;
using iTextSharp.text.pdf;



namespace Menu_Principal
{
    class Program
    {
        
      
        public static string login, senha, verif_login, Conf_Senha, id_Clinica = string.Empty;
        public static string Medico, Paciente, verif, A, texto = string.Empty;
        public static int CONT = 10, cadastrada, X, J, M = 2;
        public static DateTime Data_hora, verifHora;

        static void Main(string[] args)
        {
  
    string folder = @"\..\Registros";
           
            
            Console.BackgroundColor = ConsoleColor.White;
            Console.ForegroundColor = ConsoleColor.Black;

            if (!Directory.Exists(folder))
            {
                Directory.CreateDirectory(folder);
            }
            
            do
            {

                int i = 0;
               
                if (System.IO.File.Exists("\\..\\Registros\\Usuarios.txt"))
                {
                    if (CONT == 0)
                    {
                        Console.WriteLine("\tLogin ou senha inválidos!");
                    }
                    CONT = 0;
                   
                    Console.Write("\tDigite o usuário:");
                    login = Console.ReadLine();
                    Console.WriteLine("");
                    Console.Write("\tDigite a senha:");
                    senha = Console.ReadLine();


                    string[] array = File.ReadAllLines(@"\..\Registros\Usuarios.txt");

                    for (i = 0; i < array.Length; i++)
                    {
                        

                        

                        string[] auxiliar = array[i].Split('|');

                        verif_login = auxiliar[0];
                        Conf_Senha = auxiliar[1];
                        id_Clinica = (auxiliar[2]);
                        if ((login == verif_login) && (Conf_Senha == senha))
                        {
                            CONT = 1;

                        }

                    }

                }
              
                else
                {
                    do
                    {
                        Console.WriteLine("\tCadastre o novo usuario");

                        Console.WriteLine("\tOs codigos das clinicas são:");
                        Console.WriteLine("\t01 |Unidade de Cardiologia");
                        Console.WriteLine("\t02 |Unidade Geral");
                        Console.WriteLine("\t03 |Unidade de Pneumologia");

                        Console.Write("\tEntre com o Código da Clinica: ");
                        id_Clinica = Console.ReadLine();

                    } while (id_Clinica == "");


                    do
                    {

                        Console.WriteLine("\tO Login não pode ser vazio");

                        Console.Write("\tEntre com o Login: ");
                        login = Console.ReadLine();



                    } while (login == "");





                    Console.Write("\tEntra com a Senha: ");
                    senha = Console.ReadLine();
                    do
                    {
                        if (senha == "")
                        {
                            Console.WriteLine("\tA Senha não pode ser vazia");
                            Console.Write("\tEntre com a Senha novamente: ");
                            senha = Console.ReadLine();
                        }
                    } while (senha == "");

                    do
                    {
                        if (i == 1)
                        {
                            Console.WriteLine("\tSenha invalida");
                        }
                        Console.Write("\tConfirme a senha: ");
                        Conf_Senha = Console.ReadLine();

                        i = 1;

                    }
                    while (senha != Conf_Senha);

                    using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Usuarios.txt")))
                    {
                       
                       

                        sw.Write((login) + "|");

                        sw.WriteLine((senha) + "|" + (id_Clinica));
                        sw.Close();
                    }
                }


            } while (CONT == 0);


            Console.Clear();
            Console.WriteLine("\tLOGIN EFETUADO \n ");
            Console.WriteLine("\tSeja bem vindo !");
            Console.Read();





            do
            {
                
                Console.Clear();
                
                Console.WriteLine("");
                Console.WriteLine("\t\tUNIPMED");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t-----------------------");
                Console.WriteLine("\t-----------------------");
                Console.WriteLine("\t-----------------------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("\t\t------");
                Console.WriteLine("");
                Console.WriteLine("");
                

                Console.WriteLine("\tTecle a opção que deseja realizar e pressione Enter.");
                Console.WriteLine("\t1) Agendar Consultas ");
                Console.WriteLine("\t2) Gerar Relatorios ");
                Console.WriteLine("\t3) Cancelar Consultas");
                Console.WriteLine("\t4) Cadastro de Pacientes");
                Console.WriteLine("\t5) Cadastro de Médicos ");
                Console.WriteLine("\t6) Cadastrar Novo usuario");
                Console.WriteLine("\t7) Sair");
                Console.Write("\r\tOpção selecionada: ");
              
                A = Console.ReadLine();
                Console.Clear();
                switch (A)
                {
                   
                    case "1":
                    {
                            CONT = 0;
                            
                            do
                            {
                                if (CONT == 1)
                                {
                                    Console.WriteLine("\tPaciente não cadastrado");
                                }
                                CONT = 1;


                                Console.WriteLine("\tDigite o nome do paciente");
                                Paciente = Console.ReadLine();


                                string[] array = File.ReadAllLines(@"\..\Registros\Pacientes.txt");


                                for (int i = 0; i < array.Length; i++)
                                {

                                    string[] auxiliar = array[i].Split('|');
                                    verif = auxiliar[0];
                                    if ((Paciente == verif))
                                    {
                                        CONT = 0;

                                    }
                                }



                            } while (CONT != 0);

                            CONT = 1;
                           
                            do
                            {
                                if (CONT == 0)
                                {
                                    Console.WriteLine("\tMedico não cadastrado");
                                }
                                CONT = 0;

                                Console.WriteLine("\tDigite o nome do medico");
                                Medico = Console.ReadLine();


                                string[] array = File.ReadAllLines(@"\..\Registros\Medicos.txt");


                                for (int i = 0; i < array.Length; i++)
                                {

                                    string[] auxiliar = array[i].Split('|');
                                    verif = auxiliar[0];
                                    if ((Medico == verif))
                                    {
                                        CONT = 0;
                                    }
                                }



                            } while (CONT != 0);


                            
                            do
                            {


                                if (CONT == 1)
                                {
                                    Console.WriteLine("\tHa uma consulta marcada para esse horario");
                                }
                                else if (CONT == 2)
                                {
                                    Console.WriteLine("\tHa uma consulta marcada proxima a esse horario");
                                }

                                CONT = 0;

                                Console.WriteLine("\tDigite a data e hora da consulta (ex 00/00/0000 01:00)");
                                Data_hora = DateTime.Parse(Console.ReadLine());


                                if (System.IO.File.Exists("\\..\\Registros\\Consultas.txt"))
                                {

                                    string[] array = File.ReadAllLines(@"\..\Registros\Consultas.txt");


                                    for (int i = 0; i < array.Length; i++)
                                    {

                                        string[] auxiliar = array[i].Split('|');

                                        if (auxiliar[0] != "")
                                        {
                                            verif = auxiliar[0];
                                            verifHora = DateTime.Parse(auxiliar[2]);






                                            TimeSpan tempoPercorrido;

                                            tempoPercorrido = verifHora.Subtract(Data_hora);
                                            int Horinha, MeMATA;

                                            Horinha = tempoPercorrido.Hours;
                                            MeMATA = tempoPercorrido.Minutes;
                                            
                                            if (MeMATA < 0)
                                            {
                                                MeMATA = MeMATA * -1;
                                            }
                                            if (Horinha < 0)
                                            {
                                                Horinha = Horinha * -1;
                                            }

                                            if ((Medico == verif) && (verifHora == Data_hora))
                                            {


                                                CONT = 1;
                                            }
                                            if ((MeMATA <= 30) && (Data_hora.Date == verifHora.Date) && (Horinha == 0))
                                            {

                                                CONT = 2;
                                            }

                                        }
                                    }
                                }


                            } while (CONT != 0);

                            CONT = 2;

                            if (System.IO.File.Exists("\\..\\Registros\\Consultas.txt"))
                            {

                                string A = File.ReadAllText(@"\..\Registros\Consultas.txt");

                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Consultas.txt")))
                                {
                                    if (A != "")
                                    {
                                        sw.Write(A + "\n");
                                    }

                                    sw.Write(Medico + "|");
                                    sw.Write(Paciente + "|");
                                    sw.Write(Data_hora + "|");
                                    sw.Write(id_Clinica);
                                    sw.Close();
                                }

                            }
                            else
                            {
                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Consultas.txt")))
                                {
                                    sw.Write(Medico + "|");
                                    sw.Write(Paciente + "|");
                                    sw.Write(Data_hora + "|");
                                    sw.Write(id_Clinica);
                                    sw.Close();
                                }
                                
                            }

                            Console.WriteLine("\tConsulta cadastrada\n");
                            Console.Read();

                            break;
                        }
                    
                    case "2":
                    {
                            string B = "0";
                            Console.Clear();
                            Console.WriteLine("\tDigite uma das opçoes para a impressão de relatórios.");
                            Console.WriteLine("\t1) Relatório de Pacientes");
                            Console.WriteLine("\t2) Relatório de Consultas");
                            Console.WriteLine("\t3) Relatório dos Médicos");
                            Console.WriteLine("\t4) Relatório de Finanças");
                            Console.WriteLine("\t5) Voltar");
                            Console.Write("\r\tOpção selecionada: ");
                            B = Console.ReadLine();

                            switch (B)

                            {
                              
                                case "1":
                                    {
                                        Document doc = new Document(PageSize.A4);
                                        doc.SetMargins(40, 40, 40, 80);
                                        doc.AddCreationDate();

                                        
                                        string caminho = @"\..\Registros\Relatorio.pdf";

                                      

                                        PdfWriter writer = PdfWriter.GetInstance(doc, new
                                        FileStream(caminho, FileMode.Create));


                                        doc.Open();

                                       
                                        string dados = "";

                                        Image ImagemPdf = Image.GetInstance("Logo.png");
                                 

                                        ImagemPdf.ScaleToFit(450f, 250f);
                                        ImagemPdf.Alignment = Element.ALIGN_CENTER;
                                        doc.Add(ImagemPdf);

                                       
                                        Paragraph TItulo = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                       
                                        TItulo.Alignment = Element.ALIGN_CENTER;
                                       

                                        Paragraph TItulo2 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                      
                                        TItulo2.Alignment = Element.ALIGN_CENTER;
                                     


                                        TItulo.Add("Relatório de pacientes");
                                        TItulo.Add("\n");
                                        TItulo.Add("\n");

                                     
                                        doc.Add(TItulo);



                                        PdfPTable table = new PdfPTable(6);




                                        PdfPCell cell = new PdfPCell(new Phrase("Pacientes da Clínica de Cardiologia"));
                                        
                                        cell.FixedHeight = 30f;

                                        table.TotalWidth = 530f;
                                        table.DefaultCell.FixedHeight = 30f;


                                    

                                        table.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1; 


                                        table.AddCell(cell);

                                        table.AddCell("Id:           ");

                                        table.AddCell("Nome          ");

                                        table.AddCell("CPF           ");

                                        table.AddCell("Data          ");

                                        table.AddCell("Cep           ");

                                        table.AddCell("Telefone      ");



                                        string[] array = File.ReadAllLines(@"\..\Registros\Pacientes.txt");

                                        J = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[5] == "01")
                                            {
                                                J++;
                                                table.AddCell(Convert.ToString(J));
                                                table.AddCell(auxiliar[0]);
                                                table.AddCell(auxiliar[1]);
                                                table.AddCell(auxiliar[2]);
                                                table.AddCell(auxiliar[3]);
                                                table.AddCell(auxiliar[4]);
                                            }



                                        }



                                        TItulo2.Add("\n");



                                      
                                        PdfPTable table2 = new PdfPTable(6);




                                        cell = new PdfPCell(new Phrase("Pacientes Clínica de Geral"));
                                       
                                        cell.FixedHeight = 30f;

                                        table2.TotalWidth = 530f;
                                        table2.DefaultCell.FixedHeight = 30f;



                                        table2.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1; 

                                        table2.AddCell(cell);

                                        table2.AddCell("Id:           ");

                                        table2.AddCell("Nome          ");

                                        table2.AddCell("CPF           ");

                                        table2.AddCell("Data          ");

                                        table2.AddCell("Cep           ");

                                        table2.AddCell("Telefone      ");

                                        M = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[5] == "02")
                                            {
                                                M++;
                                                table2.AddCell(Convert.ToString(M));
                                                table2.AddCell(auxiliar[0]);
                                                table2.AddCell(auxiliar[1]);
                                                table2.AddCell(auxiliar[2]);
                                                table2.AddCell(auxiliar[3]);
                                                table2.AddCell(auxiliar[4]);
                                            }



                                        }







                                      
                                        PdfPTable table3 = new PdfPTable(6);




                                        cell = new PdfPCell(new Phrase("Pacientes Clínica de Pneumoligia "));
                                      
                                        cell.FixedHeight = 30f;



                                        table3.TotalWidth = 530f;
                                        table3.DefaultCell.FixedHeight = 30f;


                                        

                                        table3.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1; 


                                        table3.AddCell(cell);

                                        table3.AddCell("Id:           ");

                                        table3.AddCell("Nome          ");

                                        table3.AddCell("CPF           ");

                                        table3.AddCell("Data          ");

                                        table3.AddCell("Cep           ");

                                        table3.AddCell("Telefone      ");





                                        X = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[5] == "03")
                                            {
                                                
                                                X++;
                                                table3.AddCell(Convert.ToString(X));
                                                table3.AddCell(auxiliar[0]);
                                                table3.AddCell(auxiliar[1]);
                                                table3.AddCell(auxiliar[2]);
                                                table3.AddCell(auxiliar[3]);
                                                table3.AddCell(auxiliar[4]);
                                            }



                                        }





                                        PdfPTable table4 = new PdfPTable(6);




                                        cell = new PdfPCell(new Phrase("Pacientes totais de cada clínica"));
                                      
                                        cell.FixedHeight = 30f;

                                        table2.TotalWidth = 530f;
                                        table2.DefaultCell.FixedHeight = 30f;


                                       

                                        table2.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1;

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase("Clínica de cardiologia : "));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(M)));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase("Clínica de geral : "));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0;

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase(Convert.ToString(M)));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);




                                        cell = new PdfPCell(new Phrase("Clínica de Pnemologia : "));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(X)));

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 0;

                                        table4.AddCell(cell);







                                        doc.Add(table4);
                                     
                                        doc.Add(TItulo2);
                                        doc.Add(table);
                                    
                                        doc.Add(TItulo2);
                                        doc.Add(table2);
                                     
                                        doc.Add(TItulo2);
                                        doc.Add(table3);
                                       
                                        doc.Close();

                                        Console.Write("\tGerado com sucesso");
                                        Console.Read();
                                        break;
                                    }
                               
                                case "2":
                                    {
                                        String Data, dataverif;
                                        Console.Write("\tDigite o mês e o ano do qual deseja gerar o relatorio separados por uma barra \n");
                                        Data = Console.ReadLine();

                                        Document doc = new Document(PageSize.A4);
                                        doc.SetMargins(40, 40, 40, 80);

                                        doc.AddCreationDate();

                                    
                                        string caminho = @"\..\Registros\RelatorioConsultas.pdf";

                                        
                                        PdfWriter writer = PdfWriter.GetInstance(doc, new
                                        FileStream(caminho, FileMode.Create));
                                        

                                        doc.Open();

                                        
                                        string dados = "";

                                        Image ImagemPdf = Image.GetInstance("Logo.png");
                                        

                                        ImagemPdf.ScaleToFit(450f, 250f);
                                        ImagemPdf.Alignment = Element.ALIGN_CENTER;
                                        doc.Add(ImagemPdf);

                                       
                                        Paragraph TItulo = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));
                                        Paragraph TItulo3 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 14, 0));

                                        
                                        TItulo.Alignment = Element.ALIGN_CENTER;
                                        TItulo3.Alignment = Element.ALIGN_JUSTIFIED;
                                       

                                        Paragraph TItulo2 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                      
                                        TItulo2.Alignment = Element.ALIGN_CENTER;
                                      





                                        TItulo.Add("Relatório de Consultas");
                                        TItulo.Add("\n");
                                        TItulo.Add("\n");

                                        doc.Add(TItulo);



                                        PdfPTable table = new PdfPTable(4);




                                        PdfPCell cell = new PdfPCell(new Phrase("Consultas da Clínica de Cardiologia"));
                                     
                                        cell.FixedHeight = 30f;

                                        table.TotalWidth = 530f;
                                        table.DefaultCell.FixedHeight = 30f;


                                      

                                        table.LockedWidth = true;


                                        cell.Colspan = 4;

                                        cell.HorizontalAlignment = 1; 


                                        table.AddCell(cell);

                                        table.AddCell("Id:           ");

                                        table.AddCell("Médico         ");

                                        table.AddCell("Nome       ");


                                        table.AddCell("Data e hora   ");



                                        string[] array = File.ReadAllLines(@"\..\Registros\Consultas.txt");

                                        J = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "01")
                                            {


                                                string[] aux = auxiliar[2].Split('/');
                                                string[] aux2 = aux[2].Split(' ');
                                                dataverif = aux[1] + "/" + aux2[0];


                                                if (dataverif == Data)
                                                {
                                                    J++;

                                                    table.AddCell(Convert.ToString(J));
                                                    table.AddCell(auxiliar[0]);
                                                    table.AddCell(auxiliar[1]);
                                                    table.AddCell(auxiliar[2]);
                                                }

                                            }



                                        }


                                        TItulo2.Add("\n");

                                       
                                        PdfPTable table2 = new PdfPTable(4);


                                        cell = new PdfPCell(new Phrase("Consultas da Clínica de Geral"));
                                       
                                        cell.FixedHeight = 30f;

                                        table2.TotalWidth = 530f;
                                        table2.DefaultCell.FixedHeight = 30f;


                                       

                                        table2.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1; 


                                        table2.AddCell(cell);


                                        table2.AddCell("Id:           ");

                                        table2.AddCell("Médico         ");

                                        table2.AddCell("Nome       ");

                                        table2.AddCell("Data e hora   ");





                                        M = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "02")
                                            {

                                                string[] aux = auxiliar[2].Split('/');
                                                string[] aux2 = aux[2].Split(' ');
                                                dataverif = aux[1] + "/" + aux2[0];


                                                if (dataverif == Data)
                                                {
                                                    M++;
                                                    table2.AddCell(Convert.ToString(M));
                                                    table2.AddCell(auxiliar[0]);
                                                    table2.AddCell(auxiliar[1]);
                                                    table2.AddCell(auxiliar[2]);

                                                }


                                            }



                                        }









                                        PdfPTable table3 = new PdfPTable(4);




                                        cell = new PdfPCell(new Phrase("Consultas da Clínica de Pneumoligia "));
                                       
                                        cell.FixedHeight = 30f;



                                        table3.TotalWidth = 530f;
                                        table3.DefaultCell.FixedHeight = 30f;


                                    
                                        table3.LockedWidth = true;


                                        cell.Colspan = 4;

                                        cell.HorizontalAlignment = 1; 


                                        table3.AddCell(cell);


                                        table3.AddCell("Id:           ");

                                        table3.AddCell("Médico         ");

                                        table3.AddCell("Nome       ");

                                        table3.AddCell("Data e hora   ");





                                        X = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "03")
                                            {
                                                string[] aux = auxiliar[2].Split('/');
                                                string[] aux2 = aux[2].Split(' ');
                                                dataverif = aux[1] + "/" + aux2[0];


                                                if (dataverif == Data)
                                                {
                                                    X++;
                                                    table3.AddCell(Convert.ToString(X));
                                                    table3.AddCell(auxiliar[0]);
                                                    table3.AddCell(auxiliar[1]);
                                                    table3.AddCell(auxiliar[2]);
                                                }

                                            }



                                        }







                                        PdfPTable table4 = new PdfPTable(3);




                                        cell = new PdfPCell(new Phrase("Consultas totais de cada clínica"));
                                        
                                        cell.FixedHeight = 30f;





                                        table4.HorizontalAlignment = 0;

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 1;

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase("Clínica de cardiologia : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(M)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase("Clínica de geral : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase(Convert.ToString(J)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);




                                        cell = new PdfPCell(new Phrase("Clínica de Pnemologia : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(X)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);




                                        PdfPTable table5 = new PdfPTable(2);

                                        table5.HorizontalAlignment = 2;





                                        cell = new PdfPCell(new Phrase("Total Mensal"));
                                       
                                        cell.FixedHeight = 30f;

                                        table5.AddCell(cell);


                                        cell = new PdfPCell(new Phrase("Total Mensal Liquido"));
                                       
                                        cell.FixedHeight = 30f;

                                        table5.AddCell(cell);


                                        double TotalMensal;
                                       
                                        TotalMensal = M * 140;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                      


                                        TotalMensal = J * 80;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                       

                                        TotalMensal = X * 90;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);



                                        PdfPTable tablestonks = new PdfPTable(2);



                                        tablestonks.AddCell(table4);
                                        tablestonks.AddCell(table5);



                                        if ((X > M) && (X > J))
                                        {

                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Pneumologia"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);


                                        }
                                        else if ((J > M) && (J > X))
                                        {



                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Geral"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);

                                        }
                                        else
                                        {


                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Cardiologia"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);


                                        }




                                        Paragraph TItuloMensal = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                    
                                        TItuloMensal.Alignment = Element.ALIGN_JUSTIFIED;
                                       
                                        TItuloMensal.Add("Valor total da rede Mensal Bruto " + (J * 80 + M * 140 + X * 90) + ". ");
                                        TItuloMensal.Add("Valor total da rede Mensal liquido " + ((J * 80 + M * 140 + X * 90) * 0.7));

                                        tablestonks.TotalWidth = 530f;
                                        tablestonks.DefaultCell.FixedHeight = 30f;



                                        doc.Add(tablestonks);
                                        doc.Add(TItulo3);


                                     
                                        doc.Add(TItuloMensal);
                                        doc.Add(TItulo2);
                                        doc.Add(table);
                                     
                                        doc.Add(TItulo2);
                                        doc.Add(table2);
                                   
                                        doc.Add(TItulo2);
                                        doc.Add(table3);
                                       
                                        doc.Close();

                                        Console.Write("Gerado com sucesso");
                                        Console.Read();

                                        break;
                                    }
                             
                                case "3":
                                    {
                                        Document doc = new Document(PageSize.A4);
                                        doc.SetMargins(40, 40, 40, 80);
                                        doc.AddCreationDate();

                                     
                                        string caminho = @"\..\Registros\Relatorio De Medicos.pdf";

                                      

                                        PdfWriter writer = PdfWriter.GetInstance(doc, new
                                        FileStream(caminho, FileMode.Create));


                                        doc.Open();

                                     
                                        string dados = "";

                                        Image ImagemPdf = Image.GetInstance("Logo.png");
                                     

                                        ImagemPdf.ScaleToFit(450f, 250f);
                                        ImagemPdf.Alignment = Element.ALIGN_CENTER;
                                        doc.Add(ImagemPdf);

                                        
                                        Paragraph TItulo = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                        
                                        TItulo.Alignment = Element.ALIGN_CENTER;
                                       

                                        Paragraph TItulo2 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                       
                                        TItulo2.Alignment = Element.ALIGN_CENTER;
                                      


                                        TItulo.Add("Relatorio de Médicos");
                                        TItulo.Add("\n");
                                        TItulo.Add("\n");

                                   
                                        doc.Add(TItulo);



                                        PdfPTable table = new PdfPTable(7);




                                        PdfPCell cell = new PdfPCell(new Phrase("Médicos Cadastrados"));
                                    
                                        cell.FixedHeight = 30f;

                                        table.TotalWidth = 530f;
                                        table.DefaultCell.FixedHeight = 30f;


                                

                                        table.LockedWidth = true;


                                        cell.Colspan = 7;

                                        cell.HorizontalAlignment = 1; 


                                        table.AddCell(cell);

                                        table.AddCell("Id:           ");

                                        table.AddCell("Nome          ");

                                        table.AddCell("CPF           ");

                                        table.AddCell("Crm          ");

                                        table.AddCell("Data          ");

                                        table.AddCell("Cep           ");

                                        table.AddCell("Telefone      ");



                                        string[] array = File.ReadAllLines(@"\..\Registros\Medicos.txt");

                                        J = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');


                                            J++;
                                            table.AddCell(Convert.ToString(J));
                                            table.AddCell(auxiliar[0]);
                                            table.AddCell(auxiliar[1]);
                                            table.AddCell(auxiliar[2]);
                                            table.AddCell(auxiliar[3]);
                                            table.AddCell(auxiliar[4]);
                                            table.AddCell(auxiliar[5]);




                                        }

                                        doc.Add(table);
                                        doc.Close();
                                        Console.WriteLine("Gerado com sucesso");
                                        Console.Read();
                                       
                                        break;
                                    }
                         
                                case "4":
                                    {
                                        String Data, dataverif;
                                        Console.Write("\tDigite a data do qual deseja gerar o relatorio \n" +
                                            "Para o dia de hoje digite 1:\n");
                                        Data = Console.ReadLine();

                                        if (Data == "1")
                                        {
                                            Data = DateTime.Today.ToString("d/MM/yyyy");
                                        }
                                        Document doc = new Document(PageSize.A4);
                                        doc.SetMargins(40, 40, 40, 80);

                                        doc.AddCreationDate();

                                   
                                        string caminho = @"\..\Registros\RelatorioConsultasDiaria.pdf";

                                       
                                        PdfWriter writer = PdfWriter.GetInstance(doc, new
                                        FileStream(caminho, FileMode.Create));
                                       

                                        doc.Open();

                                   
                                        string dados = "";

                                        Image ImagemPdf = Image.GetInstance("Logo.png");
                                        

                                        ImagemPdf.ScaleToFit(450f, 250f);
                                        ImagemPdf.Alignment = Element.ALIGN_CENTER;
                                        doc.Add(ImagemPdf);

                                        
                                        Paragraph TItulo = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));
                                        Paragraph TItulo3 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 14, 0));

                                     
                                        TItulo.Alignment = Element.ALIGN_CENTER;
                                        TItulo3.Alignment = Element.ALIGN_JUSTIFIED;
                                       

                                        Paragraph TItulo2 = new Paragraph(dados,
                                        new Font(Font.FontFamily.TIMES_ROMAN, 16, 0));

                                     
                                        TItulo2.Alignment = Element.ALIGN_CENTER;
                                    





                                        TItulo.Add("Relatorio de Consultas");
                                        TItulo.Add("\n");
                                        TItulo.Add("\n");

                                       
                                        doc.Add(TItulo);



                                        PdfPTable table = new PdfPTable(4);




                                        PdfPCell cell = new PdfPCell(new Phrase("Consultas da Clinica de Cardiologia"));
                                     
                                        cell.FixedHeight = 30f;

                                        table.TotalWidth = 530f;
                                        table.DefaultCell.FixedHeight = 30f;


                                     

                                        table.LockedWidth = true;


                                        cell.Colspan = 4;

                                        cell.HorizontalAlignment = 1; 


                                        table.AddCell(cell);

                                        table.AddCell("Id:           ");

                                        table.AddCell("Nome          ");

                                        table.AddCell("Médico        ");


                                        table.AddCell("Data e hora   ");



                                        string[] array = File.ReadAllLines(@"\..\Registros\Consultas.txt");

                                        J = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "01")
                                            {


                                                string[] aux = auxiliar[2].Split(' ');

                                                dataverif = aux[0];


                                                if (dataverif == Data)
                                                {
                                                    J++;

                                                    table.AddCell(Convert.ToString(J));
                                                    table.AddCell(auxiliar[0]);
                                                    table.AddCell(auxiliar[1]);
                                                    table.AddCell(auxiliar[2]);
                                                }

                                            }



                                        }


                                        TItulo2.Add("\n");

                                     
                                        PdfPTable table2 = new PdfPTable(4);


                                        cell = new PdfPCell(new Phrase("Consultas da Clínica de Geral"));
                                     
                                        cell.FixedHeight = 30f;

                                        table2.TotalWidth = 530f;
                                        table2.DefaultCell.FixedHeight = 30f;


                                     

                                        table2.LockedWidth = true;


                                        cell.Colspan = 6;

                                        cell.HorizontalAlignment = 1; 


                                        table2.AddCell(cell);


                                        table2.AddCell("Id:           ");

                                        table2.AddCell("Nome          ");

                                        table2.AddCell("Médico        ");

                                        table2.AddCell("Data e hora   ");





                                        M = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "02")
                                            {


                                                string[] aux = auxiliar[2].Split(' ');

                                                dataverif = aux[0];




                                                if (dataverif == Data)
                                                {
                                                    M++;
                                                    table2.AddCell(Convert.ToString(M));
                                                    table2.AddCell(auxiliar[0]);
                                                    table2.AddCell(auxiliar[1]);
                                                    table2.AddCell(auxiliar[2]);

                                                }


                                            }



                                        }



                                     
                                        PdfPTable table3 = new PdfPTable(4);




                                        cell = new PdfPCell(new Phrase("Consultas da Clínica de Pneumoligia "));
                                      
                                        cell.FixedHeight = 30f;



                                        table3.TotalWidth = 530f;
                                        table3.DefaultCell.FixedHeight = 30f;


                                    
                                        table3.LockedWidth = true;


                                        cell.Colspan = 4;

                                        cell.HorizontalAlignment = 1; 

                                        table3.AddCell(cell);


                                        table3.AddCell("Id:           ");

                                        table3.AddCell("Nome          ");

                                        table3.AddCell("Médico        ");

                                        table3.AddCell("Data e hora   ");





                                        X = 0;

                                        for (int i = 0; i < array.Length; i++)
                                        {
                                            string[] auxiliar = array[i].Split('|');

                                            if (auxiliar[3] == "03")
                                            {


                                                string[] aux = auxiliar[2].Split(' ');

                                                dataverif = aux[0];



                                                if (dataverif == Data)
                                                {
                                                    X++;
                                                    table3.AddCell(Convert.ToString(X));
                                                    table3.AddCell(auxiliar[0]);
                                                    table3.AddCell(auxiliar[1]);
                                                    table3.AddCell(auxiliar[2]);
                                                }

                                            }



                                        }







                                        PdfPTable table4 = new PdfPTable(3);




                                        cell = new PdfPCell(new Phrase("Consultas totais de cada clinica"));
                                      
                                        cell.FixedHeight = 30f;



                                     


                                        table4.HorizontalAlignment = 0;

                                        cell.Colspan = 3;

                                        cell.HorizontalAlignment = 1; 

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase("Clinica de cardiologia : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(M)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase("Clinica de geral : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);


                                        cell = new PdfPCell(new Phrase(Convert.ToString(J)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);




                                        cell = new PdfPCell(new Phrase("Clinica de Pnemologia : "));

                                        cell.Colspan = 2;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);



                                        cell = new PdfPCell(new Phrase(Convert.ToString(X)));

                                        cell.Colspan = 1;

                                        cell.HorizontalAlignment = 0; 

                                        table4.AddCell(cell);




                                        PdfPTable table5 = new PdfPTable(2);

                                        table5.HorizontalAlignment = 2;





                                        cell = new PdfPCell(new Phrase("Total Mensal"));
                                      
                                        cell.FixedHeight = 30f;

                                        table5.AddCell(cell);


                                        cell = new PdfPCell(new Phrase("Total Mensal Liquido"));
                                   
                                        cell.FixedHeight = 30f;

                                        table5.AddCell(cell);


                                        double TotalMensal;
                                   
                                        TotalMensal = M * 140;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                   


                                        TotalMensal = J * 80;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                

                                        TotalMensal = X * 90;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);

                                        TotalMensal = TotalMensal * 0.7;
                                        cell = new PdfPCell(new Phrase(Convert.ToString(TotalMensal)));
                                        table5.AddCell(cell);



                                        PdfPTable tablestonks = new PdfPTable(2);



                                        tablestonks.AddCell(table4);
                                        tablestonks.AddCell(table5);



                                        if ((X > M) && (X > J))
                                        {

                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Pneumologia"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);


                                        }
                                        else if ((J > M) && (J > X))
                                        {



                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Geral"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);

                                        }
                                        else
                                        {


                                            cell = new PdfPCell(new Phrase(" A clínica que mais atendeu foi: Cardiologia"));
                                            cell.Colspan = 2;
                                            cell.HorizontalAlignment = 1;
                                            tablestonks.AddCell(cell);


                                        }






                                        tablestonks.TotalWidth = 530f;
                                        tablestonks.DefaultCell.FixedHeight = 30f;



                                        doc.Add(tablestonks);
                                        doc.Add(TItulo3);


                               

                                        doc.Add(TItulo2);
                                        doc.Add(table);
                                  
                                        doc.Add(TItulo2);
                                        doc.Add(table2);
                                     
                                        doc.Add(TItulo2);
                                        doc.Add(table3);
                                     
                                        doc.Close();

                                        Console.Write("Gerado com sucesso");
                                        Console.Read();

                                        break;


                                    }
                            
                                case "5":
                                    {
                                        break;
                                    }

                                default:
                                    break;
                            }

                            break;
                        }
                
                    case "3":
                    {
                            int Alt = 0;

                            string Resposta, Paciente, verif = string.Empty;
                            DateTime datahora, verifHoras;


                            Console.Write("\tDigite o nome do paciente:");
                            Paciente = Console.ReadLine();

                            Console.Write("\tDigite a data e Hora da consulta:");
                            datahora = DateTime.Parse(Console.ReadLine());




                          
                            string[] array = File.ReadAllLines(@"\..\Registros\Consultas.txt");



                            using (StreamWriter writer = new StreamWriter("\\..\\Registros\\Consultas.txt"))
                            {
                              
                                for (int i = 0; i < array.Length; i++)
                                {


                                    if (array[i] == "")
                                    {
                                        Console.Write("vazio");
                                    }

                                    string[] auxiliar = array[i].Split('|');
                                    verif = auxiliar[1];
                                    verifHoras = DateTime.Parse(auxiliar[2]);



                                    if ((Paciente == verif) && (verifHoras == datahora))
                                    {

                                        Console.Write("Deseja realmente excluir essa consulta?(sim/nao)");
                                        Resposta = Console.ReadLine();
                                      
                                        if (Resposta == "sim")
                                        {
                                            Alt = 2;
                                            Console.WriteLine("Consulta Excluida");



                                        }



                                    }
                                    else
                                    {

                                        writer.WriteLine(array[i]);
                                    }





                                }



                            }
                            if (Alt != 2)
                            {
                                Console.WriteLine("Registro não encontrado");
                                Console.Read();
                            }
                            break;
                        }
               
                    case "4":
                    {
                            string nome, cpf, data, cep, telefone = string.Empty;
                     
                            do
                            {


                                Console.WriteLine("\tO nome do paciente não pode ser vazio");

                                Console.WriteLine("\tEscreva o nome do Paciente do qual deseja cadastrar:");
                                nome = Console.ReadLine();

                            } while (nome == "");

                       
                            do
                            {


                                Console.WriteLine("\tO CPF do paciente não pode ser vazio");
                                
                                Console.WriteLine("\tEscreva o CPF do paciente do qual deseja cadastrar:");
                                cpf = Console.ReadLine();
                            } while (cpf == "");
                      
                            do
                            {


                                Console.WriteLine("\tA data não pode ser vazia ");

                                Console.WriteLine("\tEscreva a data de nascimento (usar para a separaçao ex 01/01/0001)\n ");
                                data = Console.ReadLine();
                            } while (data == "");
                   
                            do
                            {

                                Console.WriteLine("\tO cep não pode ser vazio");

                                Console.Write("\tEscreva o seu cep:");
                                cep = Console.ReadLine();
                            } while (cep == "");
                       
                            do
                            {
                                Console.WriteLine("\tO telefone não pode ser vazio");

                                Console.Write("\tEscreva o seu telefone:");
                                telefone = Console.ReadLine();
                            } while (telefone == "");

                            if (System.IO.File.Exists("\\..\\Registros\\Pacientes.txt"))
                            {
                               
                                string A = File.ReadAllText(@"\..\Registros\Pacientes.txt");

                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Pacientes.txt")))
                                {
                                    if (A != "")
                                    {
                                        sw.Write(A);
                                    }
                                    sw.Write(nome + "|");
                                    sw.Write(cpf + "|");
                                    sw.Write(data + "|");
                                    sw.Write(cep + "|");
                                    sw.Write(telefone + "|");
                                    sw.WriteLine(id_Clinica);
                                    sw.Close();
                                }

                            }
                            else
                            {
                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Pacientes.txt")))
                                {
                                    sw.Write(nome + "|");
                                    sw.Write(cpf + "|");
                                    sw.Write(data + "|");
                                    sw.Write(cep + "|");
                                    sw.Write(telefone + "|");
                                    sw.WriteLine(id_Clinica);
                                    sw.Close();
                                }

                            }

                            Console.WriteLine("Cadastrato com sucesso!");
                            Console.Read();

                            break;
                        }
               
                    case "5":
                    {
                            string nome, cpf, data, crm, cep, telefone = string.Empty;
                         
                            do
                            {


                                Console.WriteLine("\tO nome do médico não pode ser vazio");

                                Console.Write("\tEscreva o nome do medico do qual deseja cadastrar:");
                                nome = Console.ReadLine();

                            } while (nome == "");
                   

                            do
                            {


                                Console.WriteLine("\tO CPF do médico não pode ser vazio");

                                Console.WriteLine("\tEscreva o CPF do médico do qual deseja cadastrar:");
                                cpf = Console.ReadLine();
                            } while (cpf == "");
                 

                            do
                            {


                                Console.WriteLine("\tA data não pode ser vazia");

                                Console.Write("\tEscreva a data de nascimento (para separar utilizar ex 01/01/0001)\n");
                                data = Console.ReadLine();
                            } while (data == "");
                           

                            do
                            {


                                Console.WriteLine("\tO CRM não pode ser vazio");

                                Console.Write("\tEscreva o CRM:");
                                crm = Console.ReadLine();
                            } while (crm == "");
                   

                            do
                            {

                                Console.WriteLine("O cep não pode ser vazio");

                                Console.Write("\tEscreva o seu CEP:");
                                cep = Console.ReadLine();
                            } while (cep == "");
                     

                            do
                            {
                                Console.WriteLine("\tO telefone não pode ser vazio");

                                Console.Write("\tEscreva o seu telefone:");
                                telefone = Console.ReadLine();
                            } while (telefone == "");

                            if (System.IO.File.Exists("\\..\\Registros\\Medicos.txt"))
                            {

                                string A = File.ReadAllText(@"\..\Registros\Medicos.txt");

                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Medicos.txt")))
                                {
                                    if (A != "")
                                    {
                                        sw.Write(A);
                                    }
                                    sw.Write(nome + "|");
                                    sw.Write(cpf + "|");
                                    sw.Write(data + "|");
                                    sw.Write(crm + "|");
                                    sw.Write(cep + "|");
                                    sw.WriteLine(telefone);
                                    sw.Close();
                                }

                            }
                            else
                            {

                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Medicos.txt")))
                                {

                                    sw.Write(nome + "|");
                                    sw.Write(cpf + "|");
                                    sw.Write(data + "|");
                                    sw.Write(crm + "|");
                                    sw.Write(cep + "|");
                                    sw.WriteLine(telefone);
                                    sw.Close();
                                }
                            
                            }

                            Console.WriteLine("Cadastrato com sucesso!");
                            Console.Read();

                            break;

                        }
                   
                    case "6":
                    {
                       
                            int i = 0;
                            do
                            {
                                Console.WriteLine("\tCadastre o novo usuario");

                                Console.WriteLine("\tOs codigos das clinicas são:");
                                Console.WriteLine("\t01 |Unidade de Cardiologia");
                                Console.WriteLine("\t02 |Unidade Geral");
                                Console.WriteLine("\t03 |Unidade de Pneumologia");

                                Console.Write("\tEntre com o Código da Clinica: ");
                                id_Clinica = Console.ReadLine();

                            } while (id_Clinica == "");

                      
                            do
                            {

                                Console.WriteLine("\tO Login não pode ser vazio");

                                Console.Write("\tEntre com o Login: ");
                                login = Console.ReadLine();



                            } while (login == "");


                            do
                            {

                                if (System.IO.File.Exists("\\..\\Registros\\Usuarios.txt"))
                                {

                                    string[] array = File.ReadAllLines(@"\..\Registros\Usuarios.txt");

                                    for (i = 0; i < array.Length; i++)
                                    {

                                        string[] auxiliar = array[i].Split('|');
                                        verif_login = auxiliar[0];
                                        
                                        if (login == verif_login)
                                        {
                                            Console.WriteLine("Login ja cadastrado \n:");
                                            Console.Write("\tEntre com o Login novamente: ");
                                            login = Console.ReadLine();


                                        }
                                    }
                                }
                               

                            } while (login == verif_login);

                            Console.Write("\tEntra com a Senha: ");
                            senha = Console.ReadLine();
                            do
                            {
                          
                                if (senha == "")
                                {
                                    Console.WriteLine("\tA Senha não pode ser vazia");
                                    Console.Write("\tEntre com a Senha novamente: ");
                                    senha = Console.ReadLine();
                                }
                            } while (senha == "");

                            do
                            {
                                if (i == 1)
                                {
                                    Console.WriteLine("\tSenha invalida");
                                }
                                Console.Write("\tConfirme a senha:");
                                Conf_Senha = Console.ReadLine();

                                i = 1;

                            }
                            while (senha != Conf_Senha);



                            if (System.IO.File.Exists("\\..\\Registros\\Usuarios.txt"))
                            {

                                string A = File.ReadAllText(@"\..\Registros\Usuarios.txt");
                            
                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Usuarios.txt")))
                                {
                                    if (A != "")
                                    {
                                        sw.Write(A);
                                    }



                                
                                   

                                    sw.Write((login) + "|");

                                    sw.WriteLine((senha) + "|" + (id_Clinica));
                                    sw.Close();
                                }

                            }
                            else
                            {
                                using (StreamWriter sw = new StreamWriter(File.Create("\\..\\Registros\\Usuarios.txt")))
                                {

                                   

                                    sw.Write((login) + "|");

                                    sw.WriteLine((senha) + "|" + (id_Clinica));
                                    sw.Close();
                                }

                            }
                            Console.WriteLine("\tCadastrato com sucesso!");
                            Console.Read();

                            break;
                        }
                   
                    case "7":
                    {
                            Console.Clear();
                            Console.WriteLine("Saindo...");


                            break;
                        }


                    default:
                        break;



                }
            } while (A != "7");

        }
    }







  

}

