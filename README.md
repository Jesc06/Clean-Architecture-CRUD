# Clean-Architecture-CRUD
#### Clean architecture Create, Read, Update, Delete method

<br>
<br>


### 1. Display all records from the database table in the UI table

<br>

#### Create Application Interfaces

```csharp

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.Account.DTO;


namespace SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces
{
    public interface IGetAllAccounts
    {
        Task<List<StudentAccountRegistrationDTO>> GetAllAccounts();
    }
}


```

<br>



#### Create Infrastructure Repository

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces;
using SAS_Record_Management_System.Infrastructure.Persistence.Data;
using SAS_Record_Management_System.Application.Features.Account.DTO;
using Microsoft.EntityFrameworkCore;
using AutoMapper;
using AutoMapper.QueryableExtensions;
using SAS_Record_Management_System.Domain.Entities.Account;

namespace SAS_Record_Management_System.Infrastructure.Features.ViewAllStudentAccount
{
    public class GetAllAccountsRepository : IGetAllAccounts
    {
        private readonly ApplicationDbContext _context;
        public GetAllAccountsRepository(ApplicationDbContext context)
        {
            _context = context;
        }

        public async Task<List<StudentAccountRegistrationDTO>> GetAllAccounts()
        {
      
            return await _context.StudentAccountRegistrations_Db.Select(x => new StudentAccountRegistrationDTO
            {
                FirstName = x.FirstName,
                Middlename = x.Middlename,
                LastName = x.LastName,
                Gender = x.Gender,
                YearOfBirth = x.YearOfBirth,
                MonthOfBirth = x.MonthOfBirth,
                DateOfBirth = x.DateOfBirth,
                HomeAddress = x.HomeAddress,
                MobileNumber = x.MobileNumber,
                Email = x.Email,
                Program = x.Program,
                YearLevel = x.YearLevel,
                StudentID = x.StudentID,
                Password = x.Password,
            }).ToListAsync();

        }

    }
}


```


<br>



#### Create Application Services
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces;
using SAS_Record_Management_System.Application.Features.Account.DTO;

namespace SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Services
{
    public class GetAllAccountsServices 
    {
        private readonly IGetAllAccounts _getAllAccounts;
        public GetAllAccountsServices(IGetAllAccounts getAllAccounts)
        {
            _getAllAccounts = getAllAccounts;
        }

        public async Task<List<StudentAccountRegistrationDTO>> GetAllAccountsAsync()
        {
            return await _getAllAccounts.GetAllAccounts();
        }


    }
}
```

<br>


### 2. Map table data into edit UI

<br>

#### Create Application Interfaces

```csharp

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.Account.DTO;


namespace SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces
{
    public interface IGetAllAccounts
    {
        Task<StudentAccountRegistrationDTO> GetAccountById(int id);
    }
}

```

<br>

#### Create Infrastructure Repository

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces;
using SAS_Record_Management_System.Infrastructure.Persistence.Data;
using SAS_Record_Management_System.Application.Features.Account.DTO;
using Microsoft.EntityFrameworkCore;
using AutoMapper;
using AutoMapper.QueryableExtensions;

namespace SAS_Record_Management_System.Infrastructure.Features.ViewAllStudentAccount
{
    public class GetAllAccountsRepository : IGetAllAccounts
    {
        private readonly ApplicationDbContext _context;

        public GetAllAccountsRepository(ApplicationDbContext context)
        {
            _context = context;
        }

        public async Task<StudentAccountRegistrationDTO> GetAccountById(int id)
        {
            var a = _mapper.Map<StudentAccountRegistrationDTO>(
                await _context.StudentAccountRegistrations_Db.FindAsync(id)
            );
            return a;
        }

    }
}

```


<br>

#### Create Application Services
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Interfaces;
using SAS_Record_Management_System.Application.Features.Account.DTO;

namespace SAS_Record_Management_System.Application.Features.ViewAllStudentAccount.Services
{
    public class GetAllAccountsServices 
    {
        private readonly IGetAllAccounts _getAllAccounts;
        public GetAllAccountsServices(IGetAllAccounts getAllAccounts)
        {
            _getAllAccounts = getAllAccounts;
        }

  
        public async Task<StudentAccountRegistrationDTO> GetId(int id)
        {
            return await _getAllAccounts.GetAccountById(id);
        }


    }
}
```

<br>
<br>

