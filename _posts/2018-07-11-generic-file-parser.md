---
title: "Generic File Parser to extract features from Malicious Files."

category:
    - Malware

layout: single
classes: wide

tags: 
    - malware-analysis
    - pdf-parsing
    - pe-executable
    - office-files
    - reverse-engineering
    - libmagic
    - python
    - rar
    - zip
    - mime
    - machine-learning
    - static-analysis
    - dynamic-analysis
    
---

A Single Library Parser to extract meta information,static analysis and detect macros within the files.

Source Code : [Generic File Parser](https://github.com/uppusaikiran/generic-parser)

Hit Counter : [![HitCount](http://hits.dwyl.com/uppusaikiran/generic-parser.svg)](http://hits.dwyl.com/uppusaikiran/generic-parser)


# Usage:

## PreRequsite
1. Clone the Repo
2. Create a virutalenv
```
virtualenv pyenv
```
3. Install the requirements.
```
pip install -r requirements.txt
```
### Script Usage

```
(pyenv) admin@cuckoo:~/generic-parser$ python app.py -h
usage: app.py [-h] -f PATH [-s STORE] -y YARA -e EXTRACT [--version]

optional arguments:
  -h, --help            show this help message and exit
  -f PATH, --path PATH  File Absolute Path
  -s STORE, --store STORE
                        Store to DB
  -y YARA, --yara YARA  Apply Yara Matcher
  -e EXTRACT, --extract EXTRACT
                        Extract Features
  --version             show program's version number and exit

```
1. PATH  : This should point to the path of the malware file which you want to analyze.
2. STORE : Enable this flag if you want to store in a database.
3. YARA  : Enable this flag to apply yara to match for suspicious indicators in the file.
4. version : Shows the version of the tool.

### Features:

1. Ability to Identify the Decomposition module selected based on the mime-type.
2. Apply PDF based decomposition to extract features from the pdf file.
3. Apply Office based decomposition to extract features of office files.
4. Web Based files are decomposed to get interesting strings etc.
5. Yara is applied on the entire file to get interesting matches which can help in identifying suspicious behaviour.

### Sample UseCase For PDF File:

```
python app.py -f test_files/0007b52a37aef3c0cbfb96348b826fb42a48ea895fa4446ce76683fb5195f759 -y 1 -e 1
{
    "access_time": 1530781000,
    "device": 2049,
    "entropy": 0.024414521113765863,
    "features": {
        "pdf_features": {
            "comment": 1,
            "comments": [
                "oPDF.header(1.4)"
            ],
            "indirectObjects": [],
            "indirect_obj": 0,
            "names": [],
            "startXref": [],
            "start_xref": 0,
            "trailer": [],
            "xref": 0,
            "xreg": []
        }
    },
    "file_name": "0007b52a37aef3c0cbfb96348b826fb42a48ea895fa4446ce76683fb5195f759",
    "file_path": "test_files/0007b52a37aef3c0cbfb96348b826fb42a48ea895fa4446ce76683fb5195f759",
    "file_size_not_multiple_8": 7,
    "group_id_of_owner": 1000,
    "inode_number": 5379227,
    "macro": 1,
    "magic_buffer": "PDF document, version 1.4",
    "magic_info": "PDF document, version 1.4",
    "md5": "57fb493d35f33901845bbe4612faae6c",
    "meta_data_change_time": 1505571184,
    "mime": "application/pdf",
    "min_possible_file_size": 733.5831159053229,
    "modification_time": 315426600,
    "no_of_hard_links": 1,
    "protection_bytes": 33256,
    "sha1": "57fb493d35f33901845bbe4612faae6c",
    "sha256": "e1de36178b189e54ecb88497745a9b49b7e4db1e",
    "size": 30047,
    "user_id_of_owner": 1000,
    "yara": [
        "domain",
        "contentis_base64",
        "Big_Numbers3",
        "Big_Numbers1"
    ]
}

```

### Sample Use case for PE32 File
```
python app.py -f test_files/07041a3c64fea7dd888220c87ce090aa6d29c92d75ea9fce1b1d3ec98ff64cd8 -y 1 -e 1
{
    "access_time": 1530781850,
    "device": 2049,
    "entropy": 0.12669530516464111,
    "features": {
        "pe_features": {
            "anti_debugging_capabilities": [],
            "anti_vm_capabilities": [],
            "check_sum": 0,
            "compile_date": 1398238638,
            "datadir_IMAGE_DIRECTORY_ENTRY_BASERELOC_size": 131136,
            "datadir_IMAGE_DIRECTORY_ENTRY_EXPORT_size": 0,
            "datadir_IMAGE_DIRECTORY_ENTRY_IAT_size": 196,
            "datadir_IMAGE_DIRECTORY_ENTRY_IMPORT_size": 100,
            "datadir_IMAGE_DIRECTORY_ENTRY_RESOURCE_size": 14336,
            "debug_size": 0,
            "export_size": 0,
            "generated_check_sum": 984057,
            "iat_rva": 28868,
            "import_bound_symbols": [],
            "import_symbols": [
                "MsiCloseHandle",
                "SymEnumerateModules",
                "MapViewOfFileEx",
                "OleLoadPictureEx"
            ],
            "imported_symbols": [
                "dbghelp.dll:name=symgetsymfromname",
                "oleaut32.dll:name=oleicontocursor",
                "dbghelp.dll:name=symenumeratesymbols",
                "oleaut32.dll:name=safearraycreate",
                "dbghelp.dll:name=symfindfileinpath",
                "dbghelp.dll:name=symgetoptions",
                "dbghelp.dll:name=symgetlinefromname64",
                "dbghelp.dll:name=symgetlinefromaddr",
                "dbghelp.dll:name=symenumeratesymbolsw64",
                "kernel32.dll:name=mapviewoffileex",
                "kernel32.dll:name=readfile",
                "dbghelp.dll:name=symgetlinenext",
                "kernel32.dll:name=gettickcount",
                "dbghelp.dll:name=symgetsymfromaddr",
                "dbghelp.dll:name=symenumeratemodules",
                "dbghelp.dll:name=symgetmodulebase",
                "dbghelp.dll:name=symgetlinefromaddr64",
                "dbghelp.dll:name=symfromname",
                "dbghelp.dll:name=symgetlinefromname",
                "dbghelp.dll:name=symgetsearchpath",
                "dbghelp.dll:name=symenumeratesymbolsw",
                "dbghelp.dll:name=symgetmoduleinfo64",
                "kernel32.dll:name=getsystemdirectorya",
                "dbghelp.dll:name=symgetmoduleinfo",
                "dbghelp.dll:name=symgetsymfromname64",
                "dbghelp.dll:name=symgetmoduleinfow",
                "dbghelp.dll:name=symenumeratemodules64",
                "msi.dll:name=msiclosehandle",
                "dbghelp.dll:name=symfromaddr",
                "dbghelp.dll:name=symgetlinenext64",
                "oleaut32.dll:name=oleloadpictureex",
                "dbghelp.dll:name=symgetmoduleinfow64",
                "kernel32.dll:name=enumcalendarinfoa",
                "kernel32.dll:name=createfilea",
                "dbghelp.dll:name=symgetsymfromaddr64",
                "kernel32.dll:name=callnamedpipea",
                "dbghelp.dll:name=symgetlineprev64",
                "kernel32.dll:name=localalloc",
                "dbghelp.dll:name=symenumeratesymbols64",
                "dbghelp.dll:name=symfunctiontableaccess",
                "kernel32.dll:name=setconsoletitlew",
                "oleaut32.dll:name=safearraycopy",
                "dbghelp.dll:name=symgetmodulebase64",
                "dbghelp.dll:name=symgetfilelineoffsets64",
                "dbghelp.dll:name=symgetlineprev"
            ],
            "major_version": 4,
            "minor_version": 0,
            "number_of_bound_import_symbols": -1,
            "number_of_bound_imports": -1,
            "number_of_export_symbols": -1,
            "number_of_import_symbols": 45,
            "number_of_imports": 4,
            "number_of_rva_and_sizes": 16,
            "number_of_sections": 4,
            "pe_char": 15,
            "pe_dll": 0,
            "pe_driver": 0,
            "pe_exe": 1,
            "pe_i386": 1,
            "pe_majorlink": 18,
            "pe_minorlink": 8,
            "pe_warning_strings": [
                "Invalid relocation information. SizeOfBlock too large: 3431661568",
                "Corrupt header \"IMAGE_LOAD_CONFIG_DIRECTORY\" at file offset 68096. Exception: 'Data length less than expected header length.'"
            ],
            "pe_warnings": 1,
            "sec_entropy_code": 1.0860475014720217,
            "sec_entropy_data": 6.024395015352624,
            "sec_entropy_r1": 0.0,
            "sec_entropy_rdata": -1,
            "sec_entropy_reloc": -1,
            "sec_entropy_rsrc": 4.653008448519358,
            "sec_entropy_text": -1,
            "sec_raw_execsize": 124400,
            "sec_rawptr_code": 1024,
            "sec_rawptr_data": 6656,
            "sec_rawptr_r1": 30720,
            "sec_rawptr_rsrc": 16384,
            "sec_rawptr_text": -1,
            "sec_rawsize_code": 5632,
            "sec_rawsize_data": 9728,
            "sec_rawsize_r1": 4608,
            "sec_rawsize_rsrc": 14336,
            "sec_rawsize_text": -1,
            "sec_va_execsize": 34304,
            "sec_vasize_code": 20992,
            "sec_vasize_data": 82432,
            "sec_vasize_r1": 4592,
            "sec_vasize_rsrc": 16384,
            "sec_vasize_text": -1,
            "size_code": 20480,
            "size_image": 135664,
            "size_initdata": 86016,
            "size_uninit": 438272,
            "std_section_names": 0,
            "total_size_pe": 936352,
            "virtual_address": 4096,
            "virtual_size": 20992,
            "virtual_size_2": 82432
        },
        "pe_rare_features": {
            "imported_symbols": -1,
            "pe_warning_strings": -1,
            "section_names": [
                ".code",
                ".data",
                "rsrc",
                ".r1"
            ]
        }
    },
    "file_name": "07041a3c64fea7dd888220c87ce090aa6d29c92d75ea9fce1b1d3ec98ff64cd8",
    "file_path": "test_files/07041a3c64fea7dd888220c87ce090aa6d29c92d75ea9fce1b1d3ec98ff64cd8",
    "file_size_not_multiple_8": 0,
    "group_id_of_owner": 1000,
    "inode_number": 5379220,
    "macro": 1,
    "magic_buffer": "PE32 executable (GUI) Intel 80386, for MS Windows",
    "magic_info": "PE32 executable (GUI) Intel 80386, for MS Windows",
    "md5": "c7aca54886e13e3bc79a1ec4c94e7518",
    "meta_data_change_time": 1505571184,
    "mime": "application/x-dosexec",
    "min_possible_file_size": 118631.40238152204,
    "modification_time": 315426600,
    "no_of_hard_links": 1,
    "protection_bytes": 33256,
    "sha1": "c7aca54886e13e3bc79a1ec4c94e7518",
    "sha256": "96d2e1d4a451636a5997fa1e6e8f18969134004f",
    "size": 936352,
    "user_id_of_owner": 1000,
    "yara": [
        "domain",
        "win_private_profile",
        "yodas_Protector_v1033_dllocx_Ashkbiz_Danehkar_h",
        "CRC32_poly_Constant",
        "escalate_priv",
        "HasRichSignature",
        "Antivirus",
        "win_token",
        "IsPacked",
        "disable_dep",
        "contentis_base64",
        "screenshot",
        "IP",
        "win_mutex",
        "win_hook",
        "IsPE32",
        "IsWindowsGUI",
        "antisb_threatExpert",
        "win_files_operation",
        "Delphi_Copy",
        "url",
        "win_registry",
        "HasOverlay",
        "System_Tools",
        "Big_Numbers3"
    ]
}
```
