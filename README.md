using System;
using System.Collections.Generic;
using System.Drawing;
using System.Windows.Forms;

namespace HospitalSystem
{
    // Классы данных остаются такими же
    public class Patient
    {
        public int ID { get; set; }
        public string FullName { get; set; } = string.Empty;
        public string MedicalHistory { get; set; } = string.Empty;
        public DateTime AppointmentDate { get; set; }
    }

    public class Staff
    {
        public int ID { get; set; }
        public string FullName { get; set; } = string.Empty;
        public string Position { get; set; } = string.Empty;
        public string Schedule { get; set; } = string.Empty;
    }

    public class Appointment
    {
        public DateTime DateTime { get; set; }
        public Staff Doctor { get; set; } = new Staff();
        public string Room { get; set; } = string.Empty;
    }

    public class Medicine
    {
        public string Name { get; set; } = string.Empty;
        public int Stock { get; set; }
    }

    public class MainForm : Form
    {
        private DataGridView dataGridView;
        private Label titleLabel;
        private Button refreshButton;

        public MainForm()
        {
            this.Text = "Информационная система больницы";
            this.Width = 900;
            this.Height = 700;
            this.BackColor = Color.AliceBlue;

            // Заголовок
            titleLabel = new Label
            {
                Text = "Список пациентов",
                Font = new Font("Arial", 18, FontStyle.Bold),
                ForeColor = Color.DarkBlue,
                Dock = DockStyle.Top,
                Height = 40,
                TextAlign = ContentAlignment.MiddleCenter
            };
            this.Controls.Add(titleLabel);

            // Таблица
            dataGridView = new DataGridView
            {
                Dock = DockStyle.Top,
                Height = this.ClientSize.Height - 90,
                AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode.Fill,
                BackgroundColor = Color.WhiteSmoke,
                BorderStyle = BorderStyle.Fixed3D,
                ColumnHeadersDefaultCellStyle = new DataGridViewCellStyle
                {
                    BackColor = Color.LightBlue,
                    Font = new Font("Arial", 10, FontStyle.Bold),
                    Alignment = DataGridViewContentAlignment.MiddleCenter
                },
                DefaultCellStyle = new DataGridViewCellStyle
                {
                    Font = new Font("Arial", 10),
                    Alignment = DataGridViewContentAlignment.MiddleLeft
                }
            };
            this.Controls.Add(dataGridView);

            // Кнопка обновления
            refreshButton = new Button
            {
                Text = "Обновить данные",
                Font = new Font("Arial", 12),
                BackColor = Color.LightSkyBlue,
                ForeColor = Color.White,
                Dock = DockStyle.Bottom,
                Height = 40
            };
            refreshButton.Click += RefreshButton_Click;
            this.Controls.Add(refreshButton);

            // Пример данных
            var patients = new List<Patient>
            {
                new Patient { ID = 1, FullName = "Иван Иванов", MedicalHistory = "Грипп", AppointmentDate = new DateTime(2023, 12, 25, 10, 0, 0) },
                new Patient { ID = 2, FullName = "Петр Петров", MedicalHistory = "Пневмония", AppointmentDate = new DateTime(2023, 12, 25, 11, 0, 0) },
                new Patient { ID = 3, FullName = "Сергей Сергеев", MedicalHistory = "ОРВИ", AppointmentDate = new DateTime(2023, 12, 25, 12, 0, 0) },
                new Patient { ID = 4, FullName = "Анна Смирнова", MedicalHistory = "Астма", AppointmentDate = new DateTime(2023, 12, 26, 9, 0, 0) },
                new Patient { ID = 5, FullName = "Мария Кузнецова", MedicalHistory = "Гипертония", AppointmentDate = new DateTime(2023, 12, 26, 10, 0, 0) }
            };

            LoadData(patients);
        }

        private void LoadData(IEnumerable<Patient> patients)
        {
            dataGridView.DataSource = patients;
        }

        private void RefreshButton_Click(object? sender, EventArgs e)
        {
            MessageBox.Show("Данные успешно обновлены!", "Обновление", MessageBoxButtons.OK, MessageBoxIcon.Information);
        }
    }

    static class Program
    {
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new MainForm());
        }
    }
}
