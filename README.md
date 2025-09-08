<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Punjabi Education Center Management</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- React -->
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <!-- Babel Standalone -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <!-- Supabase -->
  <script src="https://unpkg.com/@supabase/supabase-js@2"></script>
  <style>
    .sidebar-transition {
      transition: all 0.3s ease;
    }
    .loading-overlay {
      background-color: rgba(255, 255, 255, 0.8);
    }
  </style>
</head>
<body class="bg-slate-100">
  <div id="root"></div>

  <script type="text/babel">
    // Supabase Initialization
    const SUPABASE_URL = 'https://albgyiurtvupvqpruxjo.supabase.co';
    const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFsYmd5aXVydHZ1cHZxcHJ1eGpvIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTUwNDg2ODEsImV4cCI6MjA3MDYyNDY4MX0.rk8xEJeZFAKiSNSL0L5L0baxAA9RW60bM6MZwe7tO58';
    
    const supabase = SUPABASE_KEY && SUPABASE_URL 
      ? supabase.createClient(SUPABASE_URL, SUPABASE_KEY) 
      : null;

    // SVG Icon Components
    const DashboardIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
      </svg>
    );

    const CenterIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
      </svg>
    );

    const TeacherIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg>
    );

    const StudentIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg>
    );

    const FinanceIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
    );

    const ReportsIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
      </svg>
    );

    const DocsIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
      </svg>
    );

    const LogoutIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
      </svg>
    );

    const MenuOpenIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
      </svg>
    );

    const MenuCloseIcon = () => (
      <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
      </svg>
    );

    // UI Components
    const Button = ({ children, onClick, className = '', ...props }) => (
      <button
        onClick={onClick}
        className={`bg-sky-500 text-white hover:bg-sky-600 px-4 py-2 rounded-md ${className}`}
        {...props}
      >
        {children}
      </button>
    );

    const Card = ({ children, className = '' }) => (
      <div className={`bg-white rounded-lg shadow-md p-6 ${className}`}>
        {children}
      </div>
    );

    const Modal = ({ isOpen, onClose, onConfirm, title, children }) => {
      if (!isOpen) return null;
      return (
        <div className="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
          <div className="bg-white rounded-lg p-6 max-w-md w-full">
            <h3 className="text-lg font-semibold mb-4">{title}</h3>
            {children}
            <div className="mt-4 flex justify-end space-x-2">
              <Button onClick={onClose} className="bg-gray-500 hover:bg-gray-600">
                Cancel
              </Button>
              <Button onClick={onConfirm} className="bg-red-500 hover:bg-red-600">
                Confirm
              </Button>
            </div>
          </div>
        </div>
      );
    };

    const SidebarItem = ({ icon, label, active, onClick }) => (
      <li
        onClick={onClick}
        className={`flex items-center p-3 rounded-md cursor-pointer ${active ? 'bg-slate-700' : 'hover:bg-slate-700'}`}
      >
        <span className="mr-3">{icon}</span>
        <span>{label}</span>
      </li>
    );

    const Sidebar = ({ isOpen, toggleSidebar, currentPage, setCurrentPage }) => {
      const menuItems = [
        { id: 'dashboard', label: 'Dashboard', icon: <DashboardIcon /> },
        { id: 'centers', label: 'Center Management', icon: <CenterIcon /> },
        { id: 'teachers', label: 'Teacher Management', icon: <TeacherIcon /> },
        { id: 'students', label: 'Student Management', icon: <StudentIcon /> },
        { id: 'finance', label: 'Financial Management', icon: <FinanceIcon /> },
        { id: 'reports', label: 'Reports & Analytics', icon: <ReportsIcon /> },
        { id: 'documents', label: 'Document Management', icon: <DocsIcon /> },
        { id: 'logout', label: 'Logout', icon: <LogoutIcon /> },
      ];

      return (
        <div
          className={`fixed md:relative z-40 w-64 h-full bg-slate-800 text-slate-100 sidebar-transition ${
            isOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
          }`}
        >
          <div className="p-4 flex justify-between items-center border-b border-slate-700">
            <h1 className="text-xl font-bold">PEC Management</h1>
            <button onClick={toggleSidebar} className="md:hidden">
              <MenuCloseIcon />
            </button>
          </div>
          <ul className="p-2">
            {menuItems.map((item) => (
              <SidebarItem
                key={item.id}
                icon={item.icon}
                label={item.label}
                active={currentPage === item.id}
                onClick={() => setCurrentPage(item.id)}
              />
            ))}
          </ul>
        </div>
      );
    };

    const LoadingOverlay = ({ isLoading }) => {
      if (!isLoading) return null;
      return (
        <div className="fixed inset-0 z-50 flex items-center justify-center loading-overlay">
          <div className="text-2xl font-semibold">Loading...</div>
        </div>
      );
    };

    const Message = ({ type, message, onClose }) => {
      if (!message) return null;
      return (
        <div
          className={`p-4 mb-4 rounded-md flex justify-between items-center ${
            type === 'error' ? 'bg-red-100 text-red-800' : 'bg-emerald-100 text-emerald-800'
          }`}
        >
          <span>{message}</span>
          {onClose && (
            <button onClick={onClose} className="ml-2">
              <svg className="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          )}
        </div>
      );
    };

    const InputField = ({ label, name, value, onChange, type = 'text', required = false, className = '', ...props }) => (
      <div className={className}>
        <label className="block text-gray-700 mb-1">{label}{required && <span className="text-red-500">*</span>}</label>
        <input
          type={type}
          name={name}
          value={value}
          onChange={onChange}
          className="w-full p-2 border rounded focus:ring-2 focus:ring-sky-500"
          required={required}
          {...props}
        />
      </div>
    );

    const SelectField = ({ label, name, value, onChange, options, required = false, className = '' }) => (
      <div className={className}>
        <label className="block text-gray-700 mb-1">{label}{required && <span className="text-red-500">*</span>}</label>
        <select
          name={name}
          value={value}
          onChange={onChange}
          className="w-full p-2 border rounded focus:ring-2 focus:ring-sky-500"
          required={required}
        >
          <option value="">Select {label}</option>
          {options.map((option) => (
            <option key={option.value} value={option.value}>
              {option.label}
            </option>
          ))}
        </select>
      </div>
    );

    // Page Components
    const DashboardPage = () => {
      const [stats, setStats] = React.useState({
        centers: 0,
        teachers: 0,
        students: 0,
        income: 0,
        expenses: 0
      });

      React.useEffect(() => {
        const fetchStats = async () => {
          try {
            // Fetch counts from Supabase
            const { count: centers } = await supabase
              .from('t_pec')
              .select('*', { count: 'exact', head: true });
            
            const { count: teachers } = await supabase
              .from('t_teacher')
              .select('*', { count: 'exact', head: true });
            
            const { count: students } = await supabase
              .from('t_student')
              .select('*', { count: 'exact', head: true });
            
            const { data: finance } = await supabase
              .from('t_finance')
              .select('amount, type');
            
            const income = finance?.filter(f => f.type === 'income').reduce((sum, f) => sum + f.amount, 0) || 0;
            const expenses = finance?.filter(f => f.type === 'expense').reduce((sum, f) => sum + f.amount, 0) || 0;

            setStats({
              centers: centers || 0,
              teachers: teachers || 0,
              students: students || 0,
              income,
              expenses
            });
          } catch (error) {
            console.error('Error fetching dashboard stats:', error);
          }
        };

        fetchStats();
      }, []);

      return (
        <div>
          <h1 className="text-2xl font-bold mb-6">Dashboard</h1>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <Card>
              <h2 className="text-xl font-semibold mb-4">Centers Overview</h2>
              <p className="text-3xl font-bold">{stats.centers}</p>
              <p className="text-gray-600 mt-2">Total Centers</p>
            </Card>
            <Card>
              <h2 className="text-xl font-semibold mb-4">Teachers Overview</h2>
              <p className="text-3xl font-bold">{stats.teachers}</p>
              <p className="text-gray-600 mt-2">Total Teachers</p>
            </Card>
            <Card>
              <h2 className="text-xl font-semibold mb-4">Students Overview</h2>
              <p className="text-3xl font-bold">{stats.students}</p>
              <p className="text-gray-600 mt-2">Total Students</p>
            </Card>
            <Card>
              <h2 className="text-xl font-semibold mb-4">Financial Overview</h2>
              <p className="text-green-600 text-2xl font-bold">₹{stats.income.toLocaleString()}</p>
              <p className="text-gray-600">Total Income</p>
              <p className="text-red-600 text-2xl font-bold mt-2">₹{stats.expenses.toLocaleString()}</p>
              <p className="text-gray-600">Total Expenses</p>
              <p className="text-2xl font-bold mt-2">₹{(stats.income - stats.expenses).toLocaleString()}</p>
              <p className="text-gray-600">Net Balance</p>
            </Card>
          </div>
        </div>
      );
    };

    // Enhanced Teacher Management Module
    const TeacherManagementPage = () => {
      const [teachers, setTeachers] = React.useState([]);
      const [centers, setCenters] = React.useState([]);
      const [isLoading, setIsLoading] = React.useState(false);
      const [message, setMessage] = React.useState({ type: '', text: '' });
      const [mode, setMode] = React.useState('list'); // 'list', 'add', 'edit', 'detail'
      const [selectedTeacher, setSelectedTeacher] = React.useState(null);
      const [deleteModalOpen, setDeleteModalOpen] = React.useState(false);
      const [formData, setFormData] = React.useState({
        name: '',
        ic_no: '',
        phone: '',
        email: '',
        qualification: '',
        join_date: '',
        center_id: '',
        address: '',
        is_active: true
      });

      const fetchTeachers = async () => {
        setIsLoading(true);
        try {
          const { data, error } = await supabase
            .from('t_teacher')
            .select('*, t_pec(pec_name)');
          
          if (error) throw error;
          setTeachers(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const fetchCenters = async () => {
        try {
          const { data, error } = await supabase
            .from('t_pec')
            .select('id, pec_name');
          
          if (error) throw error;
          setCenters(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        }
      };

      React.useEffect(() => {
        fetchTeachers();
        fetchCenters();
      }, []);

      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({ ...prev, [name]: value }));
      };

      const handleAddTeacher = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_teacher')
            .insert([formData]);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Teacher added successfully!' });
          fetchTeachers();
          setMode('list');
          setFormData({
            name: '',
            ic_no: '',
            phone: '',
            email: '',
            qualification: '',
            join_date: '',
            center_id: '',
            address: '',
            is_active: true
          });
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleUpdateTeacher = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_teacher')
            .update(formData)
            .eq('id', selectedTeacher.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Teacher updated successfully!' });
          fetchTeachers();
          setMode('detail');
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleDeleteTeacher = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_teacher')
            .delete()
            .eq('id', selectedTeacher.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Teacher deleted successfully!' });
          fetchTeachers();
          setMode('list');
          setDeleteModalOpen(false);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleViewTeacher = (teacher) => {
        setSelectedTeacher(teacher);
        setMode('detail');
      };

      const handleEditTeacher = () => {
        setFormData({
          name: selectedTeacher.name,
          ic_no: selectedTeacher.ic_no,
          phone: selectedTeacher.phone,
          email: selectedTeacher.email,
          qualification: selectedTeacher.qualification,
          join_date: selectedTeacher.join_date,
          center_id: selectedTeacher.center_id,
          address: selectedTeacher.address,
          is_active: selectedTeacher.is_active
        });
        setMode('edit');
      };

      return (
        <div>
          <div className="flex justify-between items-center mb-6">
            <h1 className="text-2xl font-bold">Teacher Management</h1>
            {mode === 'list' && (
              <Button onClick={() => setMode('add')}>Add New Teacher</Button>
            )}
            {(mode === 'add' || mode === 'edit' || mode === 'detail') && (
              <Button 
                onClick={() => {
                  setMode('list');
                  setSelectedTeacher(null);
                }}
                className="bg-slate-700 hover:bg-slate-800"
              >
                Back to List
              </Button>
            )}
          </div>

          <Message 
            type={message.type} 
            message={message.text} 
            onClose={() => setMessage({ type: '', text: '' })}
          />

          {mode === 'list' && (
            <div className="overflow-x-auto">
              <table className="min-w-full bg-white rounded-lg overflow-hidden">
                <thead className="bg-slate-100">
                  <tr>
                    <th className="py-3 px-4 text-left">Name</th>
                    <th className="py-3 px-4 text-left">IC No</th>
                    <th className="py-3 px-4 text-left">Phone</th>
                    <th className="py-3 px-4 text-left">Center</th>
                    <th className="py-3 px-4 text-left">Status</th>
                    <th className="py-3 px-4 text-left">Actions</th>
                  </tr>
                </thead>
                <tbody>
                  {teachers.map((teacher) => (
                    <tr key={teacher.id} className="border-t border-slate-200 hover:bg-slate-50">
                      <td className="py-3 px-4">{teacher.name}</td>
                      <td className="py-3 px-4">{teacher.ic_no}</td>
                      <td className="py-3 px-4">{teacher.phone}</td>
                      <td className="py-3 px-4">{teacher.t_pec?.pec_name || '-'}</td>
                      <td className="py-3 px-4">
                        <span className={`px-2 py-1 rounded-full text-xs ${teacher.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                          {teacher.is_active ? 'Active' : 'Inactive'}
                        </span>
                      </td>
                      <td className="py-3 px-4">
                        <button
                          onClick={() => handleViewTeacher(teacher)}
                          className="text-sky-500 hover:text-sky-700 mr-2"
                        >
                          View
                        </button>
                        <button
                          onClick={() => {
                            setSelectedTeacher(teacher);
                            handleEditTeacher();
                          }}
                          className="text-slate-500 hover:text-slate-700"
                        >
                          Edit
                        </button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          )}

          {(mode === 'add' || mode === 'edit') && (
            <Card>
              <h2 className="text-xl font-semibold mb-4">
                {mode === 'add' ? 'Add New Teacher' : 'Edit Teacher'}
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <InputField
                  label="Full Name"
                  name="name"
                  value={formData.name}
                  onChange={handleInputChange}
                  required
                />
                <InputField
                  label="IC Number"
                  name="ic_no"
                  value={formData.ic_no}
                  onChange={handleInputChange}
                  required
                />
                <InputField
                  label="Phone Number"
                  name="phone"
                  value={formData.phone}
                  onChange={handleInputChange}
                  required
                />
                <InputField
                  label="Email"
                  name="email"
                  type="email"
                  value={formData.email}
                  onChange={handleInputChange}
                />
                <InputField
                  label="Qualification"
                  name="qualification"
                  value={formData.qualification}
                  onChange={handleInputChange}
                />
                <InputField
                  label="Join Date"
                  name="join_date"
                  type="date"
                  value={formData.join_date}
                  onChange={handleInputChange}
                />
                <SelectField
                  label="Center"
                  name="center_id"
                  value={formData.center_id}
                  onChange={handleInputChange}
                  options={centers.map(c => ({ value: c.id, label: c.pec_name }))}
                />
                <div className="md:col-span-2">
                  <InputField
                    label="Address"
                    name="address"
                    value={formData.address}
                    onChange={handleInputChange}
                    className="md:col-span-2"
                  />
                </div>
                <div className="flex items-center">
                  <input
                    type="checkbox"
                    name="is_active"
                    id="is_active"
                    checked={formData.is_active}
                    onChange={(e) => setFormData(prev => ({ ...prev, is_active: e.target.checked }))}
                    className="mr-2"
                  />
                  <label htmlFor="is_active">Active Teacher</label>
                </div>
              </div>
              <div className="flex justify-end space-x-2 mt-6">
                <Button
                  onClick={() => setMode(mode === 'add' ? 'list' : 'detail')}
                  className="bg-gray-500 hover:bg-gray-600"
                >
                  Cancel
                </Button>
                <Button onClick={mode === 'add' ? handleAddTeacher : handleUpdateTeacher}>
                  {mode === 'add' ? 'Save Teacher' : 'Update Teacher'}
                </Button>
              </div>
            </Card>
          )}

          {mode === 'detail' && selectedTeacher && (
            <Card>
              <div className="flex justify-between items-start mb-4">
                <h2 className="text-xl font-semibold">{selectedTeacher.name}</h2>
                <div className="flex space-x-2">
                  <Button 
                    onClick={() => setDeleteModalOpen(true)}
                    className="bg-red-500 hover:bg-red-600"
                  >
                    Delete
                  </Button>
                  <Button onClick={handleEditTeacher}>
                    Edit
                  </Button>
                </div>
              </div>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <h3 className="text-lg font-medium mb-2">Personal Details</h3>
                  <div className="space-y-2">
                    <p><span className="font-medium">IC No:</span> {selectedTeacher.ic_no}</p>
                    <p><span className="font-medium">Phone:</span> {selectedTeacher.phone}</p>
                    <p><span className="font-medium">Email:</span> {selectedTeacher.email || '-'}</p>
                    <p><span className="font-medium">Qualification:</span> {selectedTeacher.qualification || '-'}</p>
                    <p><span className="font-medium">Join Date:</span> {selectedTeacher.join_date || '-'}</p>
                    <p>
                      <span className="font-medium">Status:</span> 
                      <span className={`ml-2 px-2 py-1 rounded-full text-xs ${selectedTeacher.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                        {selectedTeacher.is_active ? 'Active' : 'Inactive'}
                      </span>
                    </p>
                  </div>
                </div>
                <div>
                  <h3 className="text-lg font-medium mb-2">Center Details</h3>
                  <div className="space-y-2">
                    <p><span className="font-medium">Center:</span> {selectedTeacher.t_pec?.pec_name || '-'}</p>
                    <p><span className="font-medium">Address:</span> {selectedTeacher.address || '-'}</p>
                  </div>
                </div>
              </div>
            </Card>
          )}

          <Modal
            isOpen={deleteModalOpen}
            onClose={() => setDeleteModalOpen(false)}
            onConfirm={handleDeleteTeacher}
            title="Confirm Delete"
          >
            <p>Are you sure you want to delete teacher {selectedTeacher?.name}? This action cannot be undone.</p>
          </Modal>
        </div>
      );
    };

    // Enhanced Student Management Module
    const StudentManagementPage = () => {
      const [students, setStudents] = React.useState([]);
      const [centers, setCenters] = React.useState([]);
      const [isLoading, setIsLoading] = React.useState(false);
      const [message, setMessage] = React.useState({ type: '', text: '' });
      const [mode, setMode] = React.useState('list'); // 'list', 'add', 'edit', 'detail'
      const [selectedStudent, setSelectedStudent] = React.useState(null);
      const [deleteModalOpen, setDeleteModalOpen] = React.useState(false);
      const [formData, setFormData] = React.useState({
        name: '',
        ic_no: '',
        phone: '',
        parent_phone: '',
        center_id: '',
        class_level: '',
        join_date: '',
        address: '',
        is_active: true
      });

      const fetchStudents = async () => {
        setIsLoading(true);
        try {
          const { data, error } = await supabase
            .from('t_student')
            .select('*, t_pec(pec_name)');
          
          if (error) throw error;
          setStudents(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const fetchCenters = async () => {
        try {
          const { data, error } = await supabase
            .from('t_pec')
            .select('id, pec_name');
          
          if (error) throw error;
          setCenters(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        }
      };

      React.useEffect(() => {
        fetchStudents();
        fetchCenters();
      }, []);

      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({ ...prev, [name]: value }));
      };

      const handleAddStudent = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_student')
            .insert([formData]);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Student added successfully!' });
          fetchStudents();
          setMode('list');
          setFormData({
            name: '',
            ic_no: '',
            phone: '',
            parent_phone: '',
            center_id: '',
            class_level: '',
            join_date: '',
            address: '',
            is_active: true
          });
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleUpdateStudent = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_student')
            .update(formData)
            .eq('id', selectedStudent.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Student updated successfully!' });
          fetchStudents();
          setMode('detail');
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleDeleteStudent = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_student')
            .delete()
            .eq('id', selectedStudent.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Student deleted successfully!' });
          fetchStudents();
          setMode('list');
          setDeleteModalOpen(false);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleViewStudent = (student) => {
        setSelectedStudent(student);
        setMode('detail');
      };

      const handleEditStudent = () => {
        setFormData({
          name: selectedStudent.name,
          ic_no: selectedStudent.ic_no,
          phone: selectedStudent.phone,
          parent_phone: selectedStudent.parent_phone,
          center_id: selectedStudent.center_id,
          class_level: selectedStudent.class_level,
          join_date: selectedStudent.join_date,
          address: selectedStudent.address,
          is_active: selectedStudent.is_active
        });
        setMode('edit');
      };

      return (
        <div>
          <div className="flex justify-between items-center mb-6">
            <h1 className="text-2xl font-bold">Student Management</h1>
            {mode === 'list' && (
              <Button onClick={() => setMode('add')}>Add New Student</Button>
            )}
            {(mode === 'add' || mode === 'edit' || mode === 'detail') && (
              <Button 
                onClick={() => {
                  setMode('list');
                  setSelectedStudent(null);
                }}
                className="bg-slate-700 hover:bg-slate-800"
              >
                Back to List
              </Button>
            )}
          </div>

          <Message 
            type={message.type} 
            message={message.text} 
            onClose={() => setMessage({ type: '', text: '' })}
          />

          {mode === 'list' && (
            <div className="overflow-x-auto">
              <table className="min-w-full bg-white rounded-lg overflow-hidden">
                <thead className="bg-slate-100">
                  <tr>
                    <th className="py-3 px-4 text-left">Name</th>
                    <th className="py-3 px-4 text-left">IC No</th>
                    <th className="py-3 px-4 text-left">Phone</th>
                    <th className="py-3 px-4 text-left">Parent Phone</th>
                    <th className="py-3 px-4 text-left">Center</th>
                    <th className="py-3 px-4 text-left">Class</th>
                    <th className="py-3 px-4 text-left">Status</th>
                    <th className="py-3 px-4 text-left">Actions</th>
                  </tr>
                </thead>
                <tbody>
                  {students.map((student) => (
                    <tr key={student.id} className="border-t border-slate-200 hover:bg-slate-50">
                      <td className="py-3 px-4">{student.name}</td>
                      <td className="py-3 px-4">{student.ic_no}</td>
                      <td className="py-3 px-4">{student.phone}</td>
                      <td className="py-3 px-4">{student.parent_phone}</td>
                      <td className="py-3 px-4">{student.t_pec?.pec_name || '-'}</td>
                      <td className="py-3 px-4">{student.class_level || '-'}</td>
                      <td className="py-3 px-4">
                        <span className={`px-2 py-1 rounded-full text-xs ${student.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                          {student.is_active ? 'Active' : 'Inactive'}
                        </span>
                      </td>
                      <td className="py-3 px-4">
                        <button
                          onClick={() => handleViewStudent(student)}
                          className="text-sky-500 hover:text-sky-700 mr-2"
                        >
                          View
                        </button>
                        <button
                          onClick={() => {
                            setSelectedStudent(student);
                            handleEditStudent();
                          }}
                          className="text-slate-500 hover:text-slate-700"
                        >
                          Edit
                        </button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          )}

          {(mode === 'add' || mode === 'edit') && (
            <Card>
              <h2 className="text-xl font-semibold mb-4">
                {mode === 'add' ? 'Add New Student' : 'Edit Student'}
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <InputField
                  label="Full Name"
                  name="name"
                  value={formData.name}
                  onChange={handleInputChange}
                  required
                />
                <InputField
                  label="IC Number"
                  name="ic_no"
                  value={formData.ic_no}
                  onChange={handleInputChange}
                />
                <InputField
                  label="Phone Number"
                  name="phone"
                  value={formData.phone}
                  onChange={handleInputChange}
                />
                <InputField
                  label="Parent Phone"
                  name="parent_phone"
                  value={formData.parent_phone}
                  onChange={handleInputChange}
                  required
                />
                <SelectField
                  label="Center"
                  name="center_id"
                  value={formData.center_id}
                  onChange={handleInputChange}
                  options={centers.map(c => ({ value: c.id, label: c.pec_name }))}
                  required
                />
                <InputField
                  label="Class Level"
                  name="class_level"
                  value={formData.class_level}
                  onChange={handleInputChange}
                />
                <InputField
                  label="Join Date"
                  name="join_date"
                  type="date"
                  value={formData.join_date}
                  onChange={handleInputChange}
                />
                <div className="md:col-span-2">
                  <InputField
                    label="Address"
                    name="address"
                    value={formData.address}
                    onChange={handleInputChange}
                  />
                </div>
                <div className="flex items-center">
                  <input
                    type="checkbox"
                    name="is_active"
                    id="is_active"
                    checked={formData.is_active}
                    onChange={(e) => setFormData(prev => ({ ...prev, is_active: e.target.checked }))}
                    className="mr-2"
                  />
                  <label htmlFor="is_active">Active Student</label>
                </div>
              </div>
              <div className="flex justify-end space-x-2 mt-6">
                <Button
                  onClick={() => setMode(mode === 'add' ? 'list' : 'detail')}
                  className="bg-gray-500 hover:bg-gray-600"
                >
                  Cancel
                </Button>
                <Button onClick={mode === 'add' ? handleAddStudent : handleUpdateStudent}>
                  {mode === 'add' ? 'Save Student' : 'Update Student'}
                </Button>
              </div>
            </Card>
          )}

          {mode === 'detail' && selectedStudent && (
            <Card>
              <div className="flex justify-between items-start mb-4">
                <h2 className="text-xl font-semibold">{selectedStudent.name}</h2>
                <div className="flex space-x-2">
                  <Button 
                    onClick={() => setDeleteModalOpen(true)}
                    className="bg-red-500 hover:bg-red-600"
                  >
                    Delete
                  </Button>
                  <Button onClick={handleEditStudent}>
                    Edit
                  </Button>
                </div>
              </div>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <h3 className="text-lg font-medium mb-2">Personal Details</h3>
                  <div className="space-y-2">
                    <p><span className="font-medium">IC No:</span> {selectedStudent.ic_no || '-'}</p>
                    <p><span className="font-medium">Phone:</span> {selectedStudent.phone || '-'}</p>
                    <p><span className="font-medium">Parent Phone:</span> {selectedStudent.parent_phone || '-'}</p>
                    <p><span className="font-medium">Class Level:</span> {selectedStudent.class_level || '-'}</p>
                    <p><span className="font-medium">Join Date:</span> {selectedStudent.join_date || '-'}</p>
                    <p>
                      <span className="font-medium">Status:</span> 
                      <span className={`ml-2 px-2 py-1 rounded-full text-xs ${selectedStudent.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                        {selectedStudent.is_active ? 'Active' : 'Inactive'}
                      </span>
                    </p>
                  </div>
                </div>
                <div>
                  <h3 className="text-lg font-medium mb-2">Center Details</h3>
                  <div className="space-y-2">
                    <p><span className="font-medium">Center:</span> {selectedStudent.t_pec?.pec_name || '-'}</p>
                    <p><span className="font-medium">Address:</span> {selectedStudent.address || '-'}</p>
                  </div>
                </div>
              </div>
            </Card>
          )}

          <Modal
            isOpen={deleteModalOpen}
            onClose={() => setDeleteModalOpen(false)}
            onConfirm={handleDeleteStudent}
            title="Confirm Delete"
          >
            <p>Are you sure you want to delete student {selectedStudent?.name}? This action cannot be undone.</p>
          </Modal>
        </div>
      );
    };

    // Enhanced Financial Management Module
    const FinancialManagementPage = () => {
      const [transactions, setTransactions] = React.useState([]);
      const [centers, setCenters] = React.useState([]);
      const [isLoading, setIsLoading] = React.useState(false);
      const [message, setMessage] = React.useState({ type: '', text: '' });
      const [mode, setMode] = React.useState('list'); // 'list', 'add', 'edit'
      const [selectedTransaction, setSelectedTransaction] = React.useState(null);
      const [deleteModalOpen, setDeleteModalOpen] = React.useState(false);
      const [filter, setFilter] = React.useState({
        type: '',
        center_id: '',
        period: '',
        year: new Date().getFullYear()
      });
      const [formData, setFormData] = React.useState({
        date: new Date().toISOString().split('T')[0],
        description: '',
        amount: '',
        type: 'income',
        center_id: '',
        period: '',
        receipt_no: '',
        remarks: ''
      });

      const periods = [
        { value: 'jan-jun', label: 'January - June' },
        { value: 'jul-dec', label: 'July - December' }
      ];

      const years = Array.from({ length: 10 }, (_, i) => new Date().getFullYear() - 5 + i);

      const fetchTransactions = async () => {
        setIsLoading(true);
        try {
          let query = supabase
            .from('t_finance')
            .select('*, t_pec(pec_name)')
            .order('date', { ascending: false });

          if (filter.type) {
            query = query.eq('type', filter.type);
          }
          if (filter.center_id) {
            query = query.eq('center_id', filter.center_id);
          }
          if (filter.period) {
            query = query.eq('period', filter.period);
          }
          if (filter.year) {
            query = query.eq('year', filter.year);
          }

          const { data, error } = await query;
          
          if (error) throw error;
          setTransactions(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const fetchCenters = async () => {
        try {
          const { data, error } = await supabase
            .from('t_pec')
            .select('id, pec_name');
          
          if (error) throw error;
          setCenters(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        }
      };

      React.useEffect(() => {
        fetchTransactions();
        fetchCenters();
      }, [filter]);

      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({ ...prev, [name]: value }));
      };

      const handleFilterChange = (e) => {
        const { name, value } = e.target;
        setFilter(prev => ({ ...prev, [name]: value }));
      };

      const handleAddTransaction = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_finance')
            .insert([{
              ...formData,
              amount: parseFloat(formData.amount),
              year: filter.year
            }]);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Transaction added successfully!' });
          fetchTransactions();
          setMode('list');
          setFormData({
            date: new Date().toISOString().split('T')[0],
            description: '',
            amount: '',
            type: 'income',
            center_id: '',
            period: '',
            receipt_no: '',
            remarks: ''
          });
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleUpdateTransaction = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_finance')
            .update({
              ...formData,
              amount: parseFloat(formData.amount),
              year: filter.year
            })
            .eq('id', selectedTransaction.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Transaction updated successfully!' });
          fetchTransactions();
          setMode('list');
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleDeleteTransaction = async () => {
        setIsLoading(true);
        try {
          const { error } = await supabase
            .from('t_finance')
            .delete()
            .eq('id', selectedTransaction.id);
          
          if (error) throw error;

          setMessage({ type: 'success', text: 'Transaction deleted successfully!' });
          fetchTransactions();
          setDeleteModalOpen(false);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleEditTransaction = (transaction) => {
        setSelectedTransaction(transaction);
        setFormData({
          date: transaction.date,
          description: transaction.description,
          amount: transaction.amount,
          type: transaction.type,
          center_id: transaction.center_id,
          period: transaction.period,
          receipt_no: transaction.receipt_no,
          remarks: transaction.remarks
        });
        setMode('edit');
      };

      const calculateSummary = () => {
        const income = transactions
          .filter(t => t.type === 'income')
          .reduce((sum, t) => sum + t.amount, 0);
        
        const expenses = transactions
          .filter(t => t.type === 'expense')
          .reduce((sum, t) => sum + t.amount, 0);
        
        return {
          income,
          expenses,
          balance: income - expenses
        };
      };

      const summary = calculateSummary();

      return (
        <div>
          <div className="flex justify-between items-center mb-6">
            <h1 className="text-2xl font-bold">Financial Management</h1>
            {mode === 'list' && (
              <Button onClick={() => setMode('add')}>Add New Transaction</Button>
            )}
            {mode !== 'list' && (
              <Button 
                onClick={() => setMode('list')}
                className="bg-slate-700 hover:bg-slate-800"
              >
                Back to List
              </Button>
            )}
          </div>

          <Message 
            type={message.type} 
            message={message.text} 
            onClose={() => setMessage({ type: '', text: '' })}
          />

          {mode === 'list' && (
            <>
              <Card className="mb-6">
                <div className="grid grid-cols-1 md:grid-cols-4 gap-4">
                  <SelectField
                    label="Type"
                    name="type"
                    value={filter.type}
                    onChange={handleFilterChange}
                    options={[
                      { value: '', label: 'All Types' },
                      { value: 'income', label: 'Income' },
                      { value: 'expense', label: 'Expense' }
                    ]}
                  />
                  <SelectField
                    label="Center"
                    name="center_id"
                    value={filter.center_id}
                    onChange={handleFilterChange}
                    options={[
                      { value: '', label: 'All Centers' },
                      ...centers.map(c => ({ value: c.id, label: c.pec_name }))
                    ]}
                  />
                  <SelectField
                    label="Period"
                    name="period"
                    value={filter.period}
                    onChange={handleFilterChange}
                    options={[
                      { value: '', label: 'All Periods' },
                      ...periods
                    ]}
                  />
                  <SelectField
                    label="Year"
                    name="year"
                    value={filter.year}
                    onChange={handleFilterChange}
                    options={years.map(y => ({ value: y, label: y }))}
                  />
                </div>
              </Card>

              <Card className="mb-6">
                <h2 className="text-lg font-semibold mb-4">Financial Summary</h2>
                <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
                  <div className="bg-green-50 p-4 rounded-lg">
                    <p className="text-green-800 font-medium">Total Income</p>
                    <p className="text-2xl font-bold">₹{summary.income.toLocaleString()}</p>
                  </div>
                  <div className="bg-red-50 p-4 rounded-lg">
                    <p className="text-red-800 font-medium">Total Expenses</p>
                    <p className="text-2xl font-bold">₹{summary.expenses.toLocaleString()}</p>
                  </div>
                  <div className="bg-blue-50 p-4 rounded-lg">
                    <p className="text-blue-800 font-medium">Net Balance</p>
                    <p className={`text-2xl font-bold ${summary.balance >= 0 ? 'text-green-600' : 'text-red-600'}`}>
                      ₹{summary.balance.toLocaleString()}
                    </p>
                  </div>
                </div>
              </Card>

              <div className="overflow-x-auto">
                <table className="min-w-full bg-white rounded-lg overflow-hidden">
                  <thead className="bg-slate-100">
                    <tr>
                      <th className="py-3 px-4 text-left">Date</th>
                      <th className="py-3 px-4 text-left">Description</th>
                      <th className="py-3 px-4 text-left">Center</th>
                      <th className="py-3 px-4 text-left">Type</th>
                      <th className="py-3 px-4 text-left">Period</th>
                      <th className="py-3 px-4 text-right">Amount</th>
                      <th className="py-3 px-4 text-left">Actions</th>
                    </tr>
                  </thead>
                  <tbody>
                    {transactions.map((transaction) => (
                      <tr key={transaction.id} className="border-t border-slate-200 hover:bg-slate-50">
                        <td className="py-3 px-4">{transaction.date}</td>
                        <td className="py-3 px-4">{transaction.description}</td>
                        <td className="py-3 px-4">{transaction.t_pec?.pec_name || '-'}</td>
                        <td className="py-3 px-4">
                          <span className={`px-2 py-1 rounded-full text-xs ${transaction.type === 'income' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                            {transaction.type === 'income' ? 'Income' : 'Expense'}
                          </span>
                        </td>
                        <td className="py-3 px-4">
                          {transaction.period === 'jan-jun' ? 'Jan-Jun' : 
                           transaction.period === 'jul-dec' ? 'Jul-Dec' : '-'}
                        </td>
                        <td className={`py-3 px-4 text-right ${transaction.type === 'income' ? 'text-green-600' : 'text-red-600'}`}>
                          ₹{transaction.amount.toLocaleString()}
                        </td>
                        <td className="py-3 px-4">
                          <button
                            onClick={() => handleEditTransaction(transaction)}
                            className="text-slate-500 hover:text-slate-700"
                          >
                            Edit
                          </button>
                          <button
                            onClick={() => {
                              setSelectedTransaction(transaction);
                              setDeleteModalOpen(true);
                            }}
                            className="text-red-500 hover:text-red-700 ml-2"
                          >
                            Delete
                          </button>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            </>
          )}

          {(mode === 'add' || mode === 'edit') && (
            <Card>
              <h2 className="text-xl font-semibold mb-4">
                {mode === 'add' ? 'Add New Transaction' : 'Edit Transaction'}
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <InputField
                  label="Date"
                  name="date"
                  type="date"
                  value={formData.date}
                  onChange={handleInputChange}
                  required
                />
                <SelectField
                  label="Type"
                  name="type"
                  value={formData.type}
                  onChange={handleInputChange}
                  options={[
                    { value: 'income', label: 'Income' },
                    { value: 'expense', label: 'Expense' }
                  ]}
                  required
                />
                <InputField
                  label="Description"
                  name="description"
                  value={formData.description}
                  onChange={handleInputChange}
                  required
                />
                <InputField
                  label="Amount (₹)"
                  name="amount"
                  type="number"
                  value={formData.amount}
                  onChange={handleInputChange}
                  required
                />
                <SelectField
                  label="Center"
                  name="center_id"
                  value={formData.center_id}
                  onChange={handleInputChange}
                  options={[
                    { value: '', label: 'Select Center' },
                    ...centers.map(c => ({ value: c.id, label: c.pec_name }))
                  ]}
                />
                <SelectField
                  label="Period"
                  name="period"
                  value={formData.period}
                  onChange={handleInputChange}
                  options={[
                    { value: '', label: 'Select Period' },
                    ...periods
                  ]}
                />
                <InputField
                  label="Receipt No"
                  name="receipt_no"
                  value={formData.receipt_no}
                  onChange={handleInputChange}
                />
                <div className="md:col-span-2">
                  <InputField
                    label="Remarks"
                    name="remarks"
                    value={formData.remarks}
                    onChange={handleInputChange}
                  />
                </div>
              </div>
              <div className="flex justify-end space-x-2 mt-6">
                <Button
                  onClick={() => setMode('list')}
                  className="bg-gray-500 hover:bg-gray-600"
                >
                  Cancel
                </Button>
                <Button onClick={mode === 'add' ? handleAddTransaction : handleUpdateTransaction}>
                  {mode === 'add' ? 'Save Transaction' : 'Update Transaction'}
                </Button>
              </div>
            </Card>
          )}

          <Modal
            isOpen={deleteModalOpen}
            onClose={() => setDeleteModalOpen(false)}
            onConfirm={handleDeleteTransaction}
            title="Confirm Delete"
          >
            <p>Are you sure you want to delete this transaction? This action cannot be undone.</p>
          </Modal>
        </div>
      );
    };

    // Enhanced Reports & Analytics Module
    const ReportsPage = () => {
      const [reportType, setReportType] = React.useState('centers');
      const [period, setPeriod] = React.useState('jan-jun');
      const [year, setYear] = React.useState(new Date().getFullYear());
      const [reportData, setReportData] = React.useState(null);
      const [isLoading, setIsLoading] = React.useState(false);

      const periods = [
        { value: 'jan-jun', label: 'January - June' },
        { value: 'jul-dec', label: 'July - December' }
      ];

      const years = Array.from({ length: 5 }, (_, i) => new Date().getFullYear() - i);

      const fetchReportData = async () => {
        setIsLoading(true);
        try {
          let data;
          
          if (reportType === 'centers') {
            const { data: centers } = await supabase
              .from('t_pec')
              .select('*');
            data = centers;
          } else if (reportType === 'teachers') {
            const { data: teachers } = await supabase
              .from('t_teacher')
              .select('*, t_pec(pec_name)');
            data = teachers;
          } else if (reportType === 'students') {
            const { data: students } = await supabase
              .from('t_student')
              .select('*, t_pec(pec_name)');
            data = students;
          } else if (reportType === 'finance') {
            const { data: finance } = await supabase
              .from('t_finance')
              .select('*, t_pec(pec_name)')
              .eq('period', period)
              .eq('year', year);
            
            // Calculate summary
            const income = finance
              ?.filter(f => f.type === 'income')
              .reduce((sum, f) => sum + f.amount, 0) || 0;
            
            const expenses = finance
              ?.filter(f => f.type === 'expense')
              .reduce((sum, f) => sum + f.amount, 0) || 0;
            
            data = {
              transactions: finance,
              summary: {
                income,
                expenses,
                balance: income - expenses
              }
            };
          }

          setReportData(data);
        } catch (error) {
          console.error('Error fetching report data:', error);
        } finally {
          setIsLoading(false);
        }
      };

      React.useEffect(() => {
        fetchReportData();
      }, [reportType, period, year]);

      const renderReport = () => {
        if (!reportData) return null;

        switch (reportType) {
          case 'centers':
            return (
              <div className="overflow-x-auto">
                <table className="min-w-full bg-white rounded-lg overflow-hidden">
                  <thead className="bg-slate-100">
                    <tr>
                      <th className="py-3 px-4 text-left">Center Name</th>
                      <th className="py-3 px-4 text-left">ROS No</th>
                      <th className="py-3 px-4 text-left">Operating Days</th>
                      <th className="py-3 px-4 text-left">Bank Details</th>
                    </tr>
                  </thead>
                  <tbody>
                    {reportData.map((center) => (
                      <tr key={center.id} className="border-t border-slate-200 hover:bg-slate-50">
                        <td className="py-3 px-4">{center.pec_name}</td>
                        <td className="py-3 px-4">{center.ros_no}</td>
                        <td className="py-3 px-4">{center.day_operate} {center.time_operate}</td>
                        <td className="py-3 px-4">{center.bank_name} ({center.bank_acct_no})</td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            );
          case 'teachers':
            return (
              <div className="overflow-x-auto">
                <table className="min-w-full bg-white rounded-lg overflow-hidden">
                  <thead className="bg-slate-100">
                    <tr>
                      <th className="py-3 px-4 text-left">Name</th>
                      <th className="py-3 px-4 text-left">IC No</th>
                      <th className="py-3 px-4 text-left">Phone</th>
                      <th className="py-3 px-4 text-left">Center</th>
                      <th className="py-3 px-4 text-left">Status</th>
                    </tr>
                  </thead>
                  <tbody>
                    {reportData.map((teacher) => (
                      <tr key={teacher.id} className="border-t border-slate-200 hover:bg-slate-50">
                        <td className="py-3 px-4">{teacher.name}</td>
                        <td className="py-3 px-4">{teacher.ic_no}</td>
                        <td className="py-3 px-4">{teacher.phone}</td>
                        <td className="py-3 px-4">{teacher.t_pec?.pec_name || '-'}</td>
                        <td className="py-3 px-4">
                          <span className={`px-2 py-1 rounded-full text-xs ${teacher.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                            {teacher.is_active ? 'Active' : 'Inactive'}
                          </span>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            );
          case 'students':
            return (
              <div className="overflow-x-auto">
                <table className="min-w-full bg-white rounded-lg overflow-hidden">
                  <thead className="bg-slate-100">
                    <tr>
                      <th className="py-3 px-4 text-left">Name</th>
                      <th className="py-3 px-4 text-left">IC No</th>
                      <th className="py-3 px-4 text-left">Parent Phone</th>
                      <th className="py-3 px-4 text-left">Center</th>
                      <th className="py-3 px-4 text-left">Class</th>
                      <th className="py-3 px-4 text-left">Status</th>
                    </tr>
                  </thead>
                  <tbody>
                    {reportData.map((student) => (
                      <tr key={student.id} className="border-t border-slate-200 hover:bg-slate-50">
                        <td className="py-3 px-4">{student.name}</td>
                        <td className="py-3 px-4">{student.ic_no}</td>
                        <td className="py-3 px-4">{student.parent_phone}</td>
                        <td className="py-3 px-4">{student.t_pec?.pec_name || '-'}</td>
                        <td className="py-3 px-4">{student.class_level || '-'}</td>
                        <td className="py-3 px-4">
                          <span className={`px-2 py-1 rounded-full text-xs ${student.is_active ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                            {student.is_active ? 'Active' : 'Inactive'}
                          </span>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            );
          case 'finance':
            return (
              <div>
                <Card className="mb-6">
                  <h2 className="text-lg font-semibold mb-4">Financial Summary ({period === 'jan-jun' ? 'Jan-Jun' : 'Jul-Dec'} {year})</h2>
                  <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div className="bg-green-50 p-4 rounded-lg">
                      <p className="text-green-800 font-medium">Total Income</p>
                      <p className="text-2xl font-bold">₹{reportData.summary.income.toLocaleString()}</p>
                    </div>
                    <div className="bg-red-50 p-4 rounded-lg">
                      <p className="text-red-800 font-medium">Total Expenses</p>
                      <p className="text-2xl font-bold">₹{reportData.summary.expenses.toLocaleString()}</p>
                    </div>
                    <div className="bg-blue-50 p-4 rounded-lg">
                      <p className="text-blue-800 font-medium">Net Balance</p>
                      <p className={`text-2xl font-bold ${reportData.summary.balance >= 0 ? 'text-green-600' : 'text-red-600'}`}>
                        ₹{reportData.summary.balance.toLocaleString()}
                      </p>
                    </div>
                  </div>
                </Card>

                <div className="overflow-x-auto">
                  <table className="min-w-full bg-white rounded-lg overflow-hidden">
                    <thead className="bg-slate-100">
                      <tr>
                        <th className="py-3 px-4 text-left">Date</th>
                        <th className="py-3 px-4 text-left">Description</th>
                        <th className="py-3 px-4 text-left">Center</th>
                        <th className="py-3 px-4 text-left">Type</th>
                        <th className="py-3 px-4 text-right">Amount</th>
                      </tr>
                    </thead>
                    <tbody>
                      {reportData.transactions.map((transaction) => (
                        <tr key={transaction.id} className="border-t border-slate-200 hover:bg-slate-50">
                          <td className="py-3 px-4">{transaction.date}</td>
                          <td className="py-3 px-4">{transaction.description}</td>
                          <td className="py-3 px-4">{transaction.t_pec?.pec_name || '-'}</td>
                          <td className="py-3 px-4">
                            <span className={`px-2 py-1 rounded-full text-xs ${transaction.type === 'income' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}`}>
                              {transaction.type === 'income' ? 'Income' : 'Expense'}
                            </span>
                          </td>
                          <td className={`py-3 px-4 text-right ${transaction.type === 'income' ? 'text-green-600' : 'text-red-600'}`}>
                            ₹{transaction.amount.toLocaleString()}
                          </td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              </div>
            );
          default:
            return null;
        }
      };

      return (
        <div>
          <h1 className="text-2xl font-bold mb-6">Reports & Analytics</h1>
          
          <Card className="mb-6">
            <div className="grid grid-cols-1 md:grid-cols-4 gap-4">
              <SelectField
                label="Report Type"
                name="reportType"
                value={reportType}
                onChange={(e) => setReportType(e.target.value)}
                options={[
                  { value: 'centers', label: 'Centers Report' },
                  { value: 'teachers', label: 'Teachers Report' },
                  { value: 'students', label: 'Students Report' },
                  { value: 'finance', label: 'Financial Report' }
                ]}
              />
              
              {reportType === 'finance' && (
                <>
                  <SelectField
                    label="Period"
                    name="period"
                    value={period}
                    onChange={(e) => setPeriod(e.target.value)}
                    options={periods}
                  />
                  <SelectField
                    label="Year"
                    name="year"
                    value={year}
                    onChange={(e) => setYear(parseInt(e.target.value))}
                    options={years.map(y => ({ value: y, label: y }))}
                  />
                </>
              )}
            </div>
          </Card>

          {isLoading ? (
            <div className="flex justify-center items-center h-64">
              <div className="text-xl">Loading report data...</div>
            </div>
          ) : (
            renderReport()
          )}
        </div>
      );
    };

    // Enhanced Document Management Module
    const DocumentManagementPage = () => {
      const [documents, setDocuments] = React.useState([]);
      const [centers, setCenters] = React.useState([]);
      const [teachers, setTeachers] = React.useState([]);
      const [students, setStudents] = React.useState([]);
      const [isLoading, setIsLoading] = React.useState(false);
      const [message, setMessage] = React.useState({ type: '', text: '' });
      const [mode, setMode] = React.useState('list'); // 'list', 'upload'
      const [formData, setFormData] = React.useState({
        title: '',
        description: '',
        file: null,
        entity_type: '',
        entity_id: '',
        category: ''
      });
      const [deleteModalOpen, setDeleteModalOpen] = React.useState(false);
      const [selectedDoc, setSelectedDoc] = React.useState(null);

      const categories = [
        'Academic',
        'Administrative',
        'Financial',
        'Legal',
        'Personal',
        'Other'
      ];

      const fetchDocuments = async () => {
        setIsLoading(true);
        try {
          const { data, error } = await supabase
            .from('t_document')
            .select('*, t_pec(pec_name), t_teacher(name), t_student(name)');
          
          if (error) throw error;
          setDocuments(data);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const fetchEntities = async () => {
        try {
          const { data: centersData } = await supabase
            .from('t_pec')
            .select('id, pec_name');
          
          const { data: teachersData } = await supabase
            .from('t_teacher')
            .select('id, name');
          
          const { data: studentsData } = await supabase
            .from('t_student')
            .select('id, name');
          
          setCenters(centersData);
          setTeachers(teachersData);
          setStudents(studentsData);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        }
      };

      React.useEffect(() => {
        fetchDocuments();
        fetchEntities();
      }, []);

      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({ ...prev, [name]: value }));
      };

      const handleFileChange = (e) => {
        setFormData(prev => ({ ...prev, file: e.target.files[0] }));
      };

      const handleUploadDocument = async () => {
        if (!formData.file) {
          setMessage({ type: 'error', text: 'Please select a file to upload' });
          return;
        }

        setIsLoading(true);
        try {
          // Upload file to storage
          const fileExt = formData.file.name.split('.').pop();
          const fileName = `${Math.random()}.${fileExt}`;
          const filePath = `${fileName}`;

          const { error: uploadError } = await supabase
            .storage
            .from('documents')
            .upload(filePath, formData.file);

          if (uploadError) throw uploadError;

          // Get public URL
          const { data: { publicUrl } } = supabase
            .storage
            .from('documents')
            .getPublicUrl(filePath);

          // Save document metadata to database
          const { error: dbError } = await supabase
            .from('t_document')
            .insert([{
              title: formData.title,
              description: formData.description,
              file_url: publicUrl,
              file_name: formData.file.name,
              file_type: formData.file.type,
              file_size: formData.file.size,
              entity_type: formData.entity_type,
              entity_id: formData.entity_id,
              category: formData.category
            }]);

          if (dbError) throw dbError;

          setMessage({ type: 'success', text: 'Document uploaded successfully!' });
          fetchDocuments();
          setMode('list');
          setFormData({
            title: '',
            description: '',
            file: null,
            entity_type: '',
            entity_id: '',
            category: ''
          });
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const handleDeleteDocument = async () => {
        setIsLoading(true);
        try {
          // Delete from storage
          const filePath = selectedDoc.file_url.split('/').pop();
          await supabase
            .storage
            .from('documents')
            .remove([filePath]);

          // Delete from database
          const { error } = await supabase
            .from('t_document')
            .delete()
            .eq('id', selectedDoc.id);

          if (error) throw error;

          setMessage({ type: 'success', text: 'Document deleted successfully!' });
          fetchDocuments();
          setDeleteModalOpen(false);
        } catch (error) {
          setMessage({ type: 'error', text: error.message });
        } finally {
          setIsLoading(false);
        }
      };

      const getEntityName = (doc) => {
        if (doc.entity_type === 'center') return doc.t_pec?.pec_name;
        if (doc.entity_type === 'teacher') return doc.t_teacher?.name;
        if (doc.entity_type === 'student') return doc.t_student?.name;
        return '-';
      };

      const formatFileSize = (bytes) => {
        if (bytes === 0) return '0 Bytes';
        const k = 1024;
        const sizes = ['Bytes', 'KB', 'MB', 'GB'];
        const i = Math.floor(Math.log(bytes) / Math.log(k));
        return parseFloat((bytes / Math.pow(k, i)).toFixed(2) + ' ' + sizes[i];
      };

      return (
        <div>
          <div className="flex justify-between items-center mb-6">
            <h1 className="text-2xl font-bold">Document Management</h1>
            {mode === 'list' && (
              <Button onClick={() => setMode('upload')}>Upload Document</Button>
            )}
            {mode === 'upload' && (
              <Button 
                onClick={() => setMode('list')}
                className="bg-slate-700 hover:bg-slate-800"
              >
                Back to List
              </Button>
            )}
          </div>

          <Message 
            type={message.type} 
            message={message.text} 
            onClose={() => setMessage({ type: '', text: '' })}
          />

          {mode === 'list' && (
            <div className="overflow-x-auto">
              <table className="min-w-full bg-white rounded-lg overflow-hidden">
                <thead className="bg-slate-100">
                  <tr>
                    <th className="py-3 px-4 text-left">Title</th>
                    <th className="py-3 px-4 text-left">Category</th>
                    <th className="py-3 px-4 text-left">Linked To</th>
                    <th className="py-3 px-4 text-left">File</th>
                    <th className="py-3 px-4 text-left">Uploaded</th>
                    <th className="py-3 px-4 text-left">Actions</th>
                  </tr>
                </thead>
                <tbody>
                  {documents.map((doc) => (
                    <tr key={doc.id} className="border-t border-slate-200 hover:bg-slate-50">
                      <td className="py-3 px-4">{doc.title}</td>
                      <td className="py-3 px-4">{doc.category}</td>
                      <td className="py-3 px-4">
                        {doc.entity_type ? `${doc.entity_type}: ${getEntityName(doc)}` : '-'}
                      </td>
                      <td className="py-3 px-4">
                        <a 
                          href={doc.file_url} 
                          target="_blank" 
                          rel="noopener noreferrer"
                          className="text-sky-500 hover:text-sky-700"
                        >
                          {doc.file_name} ({formatFileSize(doc.file_size)})
                        </a>
                      </td>
                      <td className="py-3 px-4">{new Date(doc.created_at).toLocaleDateString()}</td>
                      <td className="py-3 px-4">
                        <button
                          onClick={() => {
                            setSelectedDoc(doc);
                            setDeleteModalOpen(true);
                          }}
                          className="text-red-500 hover:text-red-700"
                        >
                          Delete
                        </button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          )}

          {mode === 'upload' && (
            <Card>
              <h2 className="text-xl font-semibold mb-4">Upload Document</h2>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                <InputField
                  label="Title"
                  name="title"
                  value={formData.title}
                  onChange={handleInputChange}
                  required
                />
                <SelectField
                  label="Category"
                  name="category"
                  value={formData.category}
                  onChange={handleInputChange}
                  options={[
                    { value: '', label: 'Select Category' },
                    ...categories.map(c => ({ value: c, label: c }))
                  ]}
                  required
                />
                <div className="md:col-span-2">
                  <InputField
                    label="Description"
                    name="description"
                    value={formData.description}
                    onChange={handleInputChange}
                  />
                </div>
                <SelectField
                  label="Link To"
                  name="entity_type"
                  value={formData.entity_type}
                  onChange={handleInputChange}
                  options={[
                    { value: '', label: 'None' },
                    { value: 'center', label: 'Center' },
                    { value: 'teacher', label: 'Teacher' },
                    { value: 'student', label: 'Student' }
                  ]}
                />
                {formData.entity_type === 'center' && (
                  <SelectField
                    label="Select Center"
                    name="entity_id"
                    value={formData.entity_id}
                    onChange={handleInputChange}
                    options={[
                      { value: '', label: 'Select Center' },
                      ...centers.map(c => ({ value: c.id, label: c.pec_name }))
                    ]}
                  />
                )}
                {formData.entity_type === 'teacher' && (
                  <SelectField
                    label="Select Teacher"
                    name="entity_id"
                    value={formData.entity_id}
                    onChange={handleInputChange}
                    options={[
                      { value: '', label: 'Select Teacher' },
                      ...teachers.map(t => ({ value: t.id, label: t.name }))
                    ]}
                  />
                )}
                {formData.entity_type === 'student' && (
                  <SelectField
                    label="Select Student"
                    name="entity_id"
                    value={formData.entity_id}
                    onChange={handleInputChange}
                    options={[
                      { value: '', label: 'Select Student' },
                      ...students.map(s => ({ value: s.id, label: s.name }))
                    ]}
                  />
                )}
                <div className="md:col-span-2">
                  <label className="block text-gray-700 mb-1">File*</label>
                  <input
                    type="file"
                    onChange={handleFileChange}
                    className="w-full p-2 border rounded focus:ring-2 focus:ring-sky-500"
                    required
                  />
                </div>
              </div>
              <div className="flex justify-end space-x-2 mt-6">
                <Button
                  onClick={() => setMode('list')}
                  className="bg-gray-500 hover:bg-gray-600"
                >
                  Cancel
                </Button>
                <Button onClick={handleUploadDocument}>
                  Upload Document
                </Button>
              </div>
            </Card>
          )}

          <Modal
            isOpen={deleteModalOpen}
            onClose={() => setDeleteModalOpen(false)}
            onConfirm={handleDeleteDocument}
            title="Confirm Delete"
          >
            <p>Are you sure you want to delete document "{selectedDoc?.title}"? This action cannot be undone.</p>
          </Modal>
        </div>
      );
    };

    // Main App Component
    const App = () => {
      const [currentPage, setCurrentPage] = React.useState('dashboard');
      const [sidebarOpen, setSidebarOpen] = React.useState(false);
      const [loading, setLoading] = React.useState(false);
      const [message, setMessage] = React.useState({ type: '', text: '' });

      const toggleSidebar = () => setSidebarOpen(!sidebarOpen);

      const renderPage = () => {
        switch (currentPage) {
          case 'dashboard':
            return <DashboardPage />;
          case 'centers':
            return <CenterManagementPage />;
          case 'teachers':
            return <TeacherManagementPage />;
          case 'students':
            return <StudentManagementPage />;
          case 'finance':
            return <FinancialManagementPage />;
          case 'reports':
            return <ReportsPage />;
          case 'documents':
            return <DocumentManagementPage />;
          case 'logout':
            return <div>Logging out...</div>;
          default:
            return <DashboardPage />;
        }
      };

      return (
        <div className="min-h-screen flex">
          {!SUPABASE_URL || !SUPABASE_KEY ? (
            <div className="bg-red-100 text-red-800 p-4">
              Error: Supabase URL or Key is missing. Please check your configuration.
            </div>
          ) : (
            <>
              <Sidebar
                isOpen={sidebarOpen}
                toggleSidebar={toggleSidebar}
                currentPage={currentPage}
                setCurrentPage={setCurrentPage}
              />
              <div className="flex-1 md:ml-64">
                <div className="p-4 md:p-6">
                  <button
                    onClick={toggleSidebar}
                    className="md:hidden mb-4 p-2 rounded-md bg-slate-200"
                  >
                    <MenuOpenIcon />
                  </button>
                  {renderPage()}
                </div>
              </div>
              <LoadingOverlay isLoading={loading} />
            </>
          )}
        </div>
      );
    };

    // Render the app
    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>
